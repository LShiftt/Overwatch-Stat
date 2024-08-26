<script setup>
const copyText = (event) => {
  const liElement = event.target.closest('li');
  const textToCopy = liElement ? liElement.innerText : '';
  navigator.clipboard.writeText(textToCopy).then(() => {
    console.log('Text copied : ', textToCopy);
  }).catch(err => {
    console.error('Error : ', err);
  });
};
</script>

<template>
  <input type="button" value="Copy" @click="copyText">
</template>

<style scoped>
input[type="button"] {
  cursor: pointer;
  margin-left: 10px;
}
</style>
