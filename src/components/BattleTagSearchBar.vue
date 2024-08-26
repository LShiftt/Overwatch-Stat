<script setup>
import { ref, reactive } from "vue";
import BoldItalic from "./BoldItalic.vue";

const battleTagUser = ref("");
const profileData = reactive({
  ratings: [
    {
      role: "",
      roleIcon: "",
      group: "",
      tier: "",
      divisionIcon: "",
      rankIcon: "",
      status: "",
    },
    {
      role: "",
      roleIcon: "",
      group: "",
      tier: "",
      divisionIcon: "",
      rankIcon: "",
      status: "",
    },
    {
      role: "",
      roleIcon: "",
      group: "",
      tier: "",
      divisionIcon: "",
      rankIcon: "",
      status: "",
    },
    {
      role: "",
      roleIcon: "",
      group: "",
      tier: "",
      divisionIcon: "",
      rankIcon: "",
      status: "",
    },
  ],
});

const ready = ref(false);
const error = ref("");

function resetProfileData() {
  profileData.private = "";
  profileData.name = "";
  profileData.icon = "";
  profileData.endorsement = "";
  profileData.endorsementIcon = "";
  profileData.gamesWon = "";
  profileData.gamesLost = "";
  profileData.gameRatio = "";
  profileData.gamesPlayed = "";
  profileData.ratings.forEach((rating) => {
    rating.role = "";
    rating.roleIcon = "";
    rating.group = "";
    rating.tier = "";
    rating.divisionIcon = "";
    rating.rankIcon = "";
    rating.status = "";
  });
}

async function getProfile() {
  try {
    error.value = "";
    const response = await fetch(
      "https://ow-api.com/v1/stats/pc/eu/" + battleTagUser.value + "/profile"
    );
    if (!response.ok) {
      throw new Error("Failed to fetch profile data.");
    }
    const profile = await response.json();
    resetProfileData();
    console.log(profile);

    profileData.private = profile.private;
    profileData.name = profile.name;
    profileData.icon = profile.icon;
    profileData.endorsement = profile.endorsement;
    profileData.endorsementIcon = profile.endorsementIcon;
    profileData.gamesWon = profile.gamesWon;
    profileData.gamesLost = profile.gamesLost;
    profileData.gameRatio = profileData.gamesWon - profileData.gamesLost;
    profileData.gameRatio =
      profileData.gameRatio > 0
        ? "+" + profileData.gameRatio
        : "" + profileData.gameRatio;
    profileData.gamesPlayed = profile.gamesPlayed;
    if (Array.isArray(profile.ratings)) {
      profile.ratings.forEach((rating, index) => {
        if (index < profileData.ratings.length) {
          profileData.ratings[index].role = rating.role;
          profileData.ratings[index].roleIcon = rating.roleIcon;
          profileData.ratings[index].group = rating.group;
          profileData.ratings[index].tier = rating.tier;
          profileData.ratings[index].divisionIcon = rating.divisionIcon;
          profileData.ratings[index].rankIcon = rating.rankIcon;
        }
      });

      for (let i = profile.ratings.length; i < profileData.ratings.length; i++) {
        profileData.ratings[i].status = "empty";
      }
    } else {
      profileData.ratings.forEach(rating => {
        rating.status = "empty";
      });
    }
    if (!ready.value) {
      ready.value = true;
    }
    console.dir(profileData);

  } catch (err) {
    console.log(err);
    error.value = "An error occurred while fetching the profile data. Please check the BattleTag and try again.";
  }
}
</script>


<template>
  <div id="battleTagSearchDiv">
    <input type="text" v-model="battleTagUser" placeholder="Enter BattleTag with a - instead of a # (Player-1234)" />
    <button @click="getProfile">Search</button>
  </div>

  <div v-if="ready" id="result">
    <img :src="profileData.icon" />

    <h1>{{ profileData.name }}</h1>
    <img :src="profileData.endorsementIcon" :alt="'Overwatch\'s endorsement picture level ' + profileData.endorsement"
      style="max-width: 65px" />

    <ul>
      <li>Matches played : {{ profileData.gamesPlayed }}</li>
      <li>Matches won : {{ profileData.gamesWon }}</li>
      <li>Matches lost : {{ profileData.gamesLost }}</li>
      <li>W/L ratio : {{ profileData.gameRatio }}</li>
    </ul>
    <section>
      <div v-for="(rating, index) in profileData.ratings" :key="index">
        <div v-if="rating.status == 'empty'">
          <p>Unable to access the player's ratings. If this is your account, please complete your placement games.</p>
        </div>
        <div v-else>
          <img :src="rating.roleIcon" :alt="'Overwatch\'s logo for the ' + rating.role + ' role'" />
          <h3>Role: {{ rating.role }}</h3>
          <img :src="rating.rankIcon" :alt="'Overwatch\'s logo for the rank ' + rating.group" />
          <h3>Rank: {{ rating.group }}</h3>
          <img :src="rating.divisionIcon" :alt="'Overwatch\'s logo for division ' + rating.tier" />
          <h3>Division: {{ rating.tier }}</h3>
        </div>
      </div>
    </section>
  </div>

  <!-- Affichage de l'erreur -->
  <div v-if="error" id="error">
    <p>
      <BoldItalic :msg="error" />
    </p>
  </div>
</template>



<style scoped>
#battleTagSearchDiv {
  display: flex;
  flex-flow: row wrap;
  justify-content: center;
  align-items: center;
  min-width: 230px;
  margin-bottom: 1em;
}


#result {
  background-color: darkslategrey;
  display: flex;
  flex-flow: row wrap;
  justify-content: space-evenly;
  align-items: center;
  padding: 1rem;
  min-width: 230px;
}

#result>section {
  background-color: darkslategrey;
  display: flex;
  flex-flow: row wrap;
  justify-content: space-around;
  align-items: center;
  padding: 0.5rem;
}

#result>section>div {
  display: flex;
  flex-flow: column nowrap;
  justify-content: space-around;
  align-items: center;
  padding: 1rem;
  text-align: center;
  border: solid 2px;
  border-radius: 7px;
  margin: 1rem;
  height: fit-content;
}

section img {
  max-width: 80px;
}
</style>
