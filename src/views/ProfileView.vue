<script setup>
import BoldItalic from "../components/BoldItalic.vue";
import SearchBar from "../components/BattleTagSearchBar.vue";



</script>

<template>
      <h1>Please enter your BattleTag.</h1>
      <h2>Here some exemples you can freely use if needed :</h2>
      <h3>My friend's and my accounts</h3>
      <ol>
        <li><BoldItalic msg="LShift-21585"/></li>
        <li><BoldItalic msg="RShift-21343"/></li>
        <li><BoldItalic msg="GoldCobra-21360"/></li>
        <li><BoldItalic msg="aRIN-21470"/></li>
        <li><BoldItalic msg="IMU-21174"/></li>
        <li><BoldItalic msg="Faye-22702"/></li>
        <li><BoldItalic msg="Titoune-21156"/></li>
      </ol>
      <h3>Some randoms player's accounts</h3>
      <ol>
        <li><BoldItalic msg="Lambolauro-2396"/></li>
        <li><BoldItalic msg="pge-11208"/></li>
        <li><BoldItalic msg="eyekenspel-1604"/></li>
      </ol>
 <SearchBar/>
</template>

<style scoped></style>
