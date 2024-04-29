<script setup>
const props=defineProps(['userAlternative', 'computerAlternative', 'winnerInfo' ])
</script>
<template>
    <div v-if="props.winnerInfo !==''" id="result">
        <p>du valde {{props.userAlternative}}</p>
        <p> datorn valde {{props.computerAlternative}}</p>
        <p>{{ props.winnerInfo }}</p>
  </div>
  </template>

  <style scoped>
   #result p {
    margin: auto;
    width: 50%;
    background-color: rgb(255, 189, 189);
    padding: 0.5em;
  }
  
</style>