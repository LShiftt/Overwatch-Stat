<script setup>
import BoldItalic from "../components/BoldItalic.vue";
import SearchBar from "../components/BattleTagSearchBar.vue";
import CopyButton from "../components/CopyButton.vue";



</script>

<template>
  <h1>Please enter your BattleTag.</h1>
  <h2>Here some exemples you can freely use if needed :</h2>
  <section>
    <h3>My friend's and my accounts</h3>
    <ol>
      <li>
        <BoldItalic msg="LShift-21585" />
        <CopyButton />
      </li>
      <li>
        <BoldItalic msg="RShift-21343" />
        <CopyButton />
      </li>
      <li>
        <BoldItalic msg="GoldCobra-21360" />
        <CopyButton />
      </li>
      <li>
        <BoldItalic msg="aRIN-21470" />
        <CopyButton />
      </li>
      <li>
        <BoldItalic msg="IMU-21174" />
        <CopyButton />
      </li>
      <li>
        <BoldItalic msg="Faye-22702" />
        <CopyButton />
      </li>
      <li>
        <BoldItalic msg="Titoune-21156" />
        <CopyButton />
      </li>
    </ol>
  </section>
  <section>
    <h3>Some randoms player's accounts</h3>
    <ol>
      <li>
        <BoldItalic msg="eyekenspel-1604" />
        <CopyButton />
      </li>
      <li>
        <BoldItalic msg="pge-11208" />
        <CopyButton />
      </li>
      <li>
        <BoldItalic msg="Lambolauro-2396" />
        <CopyButton />
      </li>
    </ol>
  </section>
  <section class="searchBar">
    <SearchBar />
  </section>
</template>

<style scoped>
*{
  padding: 4px;
}
span{
  padding-right: 2em;
}
h3{
  padding: 0px;
}
li{
  white-space: nowrap;
  padding: 6px;
}
</style>
