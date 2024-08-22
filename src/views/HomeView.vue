<script setup>
import BoldItalic from "../components/BoldItalic.vue";
import Button from 'primevue/button';

</script>

<template>
  <h1>Welcome to <span>Overwatch Stat</span>, a web app to retrieve your data from <BoldItalic msg="Overwatch2"/>.</h1>
  <h2>This app have been made <BoldItalic msg="Dubois Mathis"/>, a web student and a gamer 🎮 in order to try <BoldItalic msg="Vite.js"/> & <BoldItalic msg="Vue.js"/>.</h2>
<br>
<h3>This app ins't affiliated in any way to <BoldItalic msg="Overwatch2"/> from <BoldItalic msg="Blizzard Entertainment"/>.</h3>
<Button as="router-link" label="Get Started" to="/profile" />
</template>

<style scoped>
span{
  font-weight: bold;
}
</style>
