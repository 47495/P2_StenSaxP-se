<script setup>
import { ref } from 'vue'
import GameAlternatives from './components/GameAlternatives.vue'; 
import GameScore from './components/GameScore.vue';
import GameResult from './components/GameResult.vue';
import GameStats from './components/GameStats.vue';

  const alternative=ref('')
  const compAlternative=ref('')
  const winnerInfo=ref('')
  const winner=ref('')
  const round = ref(0)
  const itemWins = ref({scissors: 0, paper: 0, rock: 0})
  
function setWinnerInfo (_winner) { //funktion som uppdaterar vinnaren
  winner.value=_winner //uppdatera vinnare
  round.value++
  if (_winner === 'draw') { //om det blir oavgjort
   winnerInfo.value="oavgjort!" //visa meddelande
  
  } else if ( _winner === 'user') { //om användare vinnare 
    winnerInfo.value= "du vann! (fusk?)" //visa meddelande 
  } else {
    winnerInfo.value="datorn vann! (L)" //annars visa dator vann meddelande 
  }
}
  function setUserAlternative(alt) {
    alternative.value=alt
  }
  function setComputerAlternative(alt) {
    compAlternative.value = alt
  }

  function updateWinItems(item) {
    itemWins.value[item] += 1
  }
</script>

<template>
  <h1>sten sax påse</h1>
  <GameStats :alternatives="itemWins" />
  <GameAlternatives
   @user-choice="setUserAlternative" 
   @computer-choice="setComputerAlternative" 
   @winner="setWinnerInfo"
   @win-item="updateWinItems"
   />
   <GameScore
   :user-alternative="alternative"
   :computer-alternative="compAlternative"
   :winner-info="winnerInfo"
    />
  <GameResult :result="{ round, winner}" />
</template>

<style scoped>
  h1{
    text-align: center;
    min-width: 10px;
  }
  #result p {
    margin: auto;
    width: 50%;
    background-color: rgb(255, 189, 189);
    padding: 0.5em;
  }
  
</style>
