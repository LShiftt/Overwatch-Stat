<script setup>
defineProps({
  msg: {
    type: String,
    required: true
  }
})
</script>

<template>
    <span>{{ msg }}</span>
</template>

<style scoped>
span{
    font-weight: bold;
    font-style: italic;
}
</style>
