<script setup>
import { ref, reactive } from "vue";

const battleTagUser = ref("");
const profileData = reactive({
  private: "",
  name: "",
  icon: "",
  endorsement: "",
  endorsementIcon: "",
  gamesWon: "",
  gamesLost: "",
  gameRatio: "",
  gamesPlayed: "",
  ratings: [
    {
      role: "",
      roleIcon: "",
      group: "",
      tier: "",
      divisionIcon: "",
      rankIcon: "",
    },
    {
      role: "",
      roleIcon: "",
      group: "",
      tier: "",
      divisionIcon: "",
      rankIcon: "",
    },
    {
      role: "",
      roleIcon: "",
      group: "",
      tier: "",
      divisionIcon: "",
      rankIcon: "",
    },
  ],
});
const ready = ref(false);

async function getProfile() {
  try {
    const response = await fetch(
      "https://ow-api.com/v1/stats/pc/eu/" + battleTagUser.value + "/profile"
    );
    const profile = await response.json();
    console.log(profile);

    profileData.private = profile.private;
    profileData.name = profile.name;
    profileData.icon = profile.icon;
    profileData.endorsement = profile.endorsement;
    profileData.endorsementIcon = profile.endorsementIcon;
    profileData.gamesWon = profile.gamesWon;
    profileData.gamesLost = profile.gamesLost;
    profileData.gameRatio = profileData.gamesWon - profileData.gamesLost; //suite
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
    }
    ready.value = !ready.value;
    console.dir(profileData);
  } catch (error) {
    console.log(error);
  }
}
</script>

<template>
  <div id="battleTagSearchDiv">
    <input
      type="text"
      v-model="battleTagUser"
      placeholder="Enter BattleTag with a - instead of a #( Player-1234)"
    />
    <button @click="getProfile">Search</button>
  </div>
  <div v-if="ready" id="result">
    <img :src="profileData.icon" />

      <h1>{{ profileData.name }}</h1>
      <img
        :src="profileData.endorsementIcon"
        :alt="
          'Overwatch\'s endorsement picture level ' + profileData.endorsement
        "
        style="max-width: 65px"
      />

    <ul>
      <li>Matches played : {{ profileData.gamesPlayed }}</li>
      <li>Matches won : {{ profileData.gamesWon }}</li>
      <li>Matches lost : {{ profileData.gamesLost }}</li>
      <li>W/L ratio : {{ profileData.gameRatio }}</li>
    </ul>
    <!-- il y a parfois un bug dans l'image utiliser lors du premier role  -->
    <section>
      <div v-for="(rating, index) in profileData.ratings" :key="index">
        <img
          :src="rating.roleIcon"
          :alt="'Overwatch\'s logo for the ' + rating.role + ' role'"
        />
        <h3>Role: {{ rating.role }}</h3>
        <img
          :src="rating.rankIcon"
          :alt="'Overwatch\'s logo for the rank ' + rating.group"
        />
        <h3>Rank: {{ rating.group }}</h3>
        <img
          :src="rating.divisionIcon"
          :alt="'Overwatch\'s logo for division ' + rating.tier"
        />
        <h3>Division: {{ rating.tier }}</h3>
      </div>
    </section>
  </div>
</template>

<style scoped>
#result {
  background-color: darkslategrey;
  display: flex;
  flex-flow: row wrap;
  justify-content: space-evenly;
  align-items: center;
  padding: 1rem;
}
#result > section {
  background-color: darkslategrey;
  display: flex;
  flex-flow: row wrap;
  justify-content: space-evenly;
  align-items: center;
  padding: 0.5rem;
}
#result > section > div {
  display: flex;
  flex-flow: column nowrap;
  justify-content: space-around;
  align-items: center;
  padding: 1rem;
  text-align: center;
  border: solid 2px;
  border-radius: 7px;
  margin: 1rem;
}
section img {
  max-width: 80px;
}
</style>
