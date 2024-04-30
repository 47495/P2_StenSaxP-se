<script setup>
import { defineProps, ref, watch } from 'vue'; //importerar funktioner från vue

const prop = defineProps(['result'])  // Definiera egenskapen 'result'.
const userScore = ref(0) //Skapa en referens för användarens poäng. 
const computerScore = ref(0)  //Skapa en referens för datorns poäng.

watch (prop,() =>{ // håller koll på ändringar i 'result'
    if (prop.result.winner === 'user') { //om användaren vinner
        userScore.value++//öka användarens poäng med 1
    } else if (prop.result.winner === 'computer') { //om datorn vinner
        computerScore.value++ //öka datorns poäng med 1
    }
})

</script>

<template>
    <div v-if="computerScore || userScore">
    <span id="userScore"> 
        <span :class="userScore > computerScore ? 'leader score' : 'score'">{{ userScore }}</span>
        <p v-if="computerScore > userScore">Loser</p>
        <p v-else>User</p>

    </span>

    <span id="computerScore"> 
        <span :class="userScore < computerScore ? 'leader score' : 'score'">{{ computerScore }}</span>
        <p>Computer</p> 
    </span>
</div>
</template>

<style scoped> 
div {
    margin: auto;
    padding: 0.5em;
    width:50%;
    display:flex;
    justify-content: center;

}
.score{
    background-color: rgb(98, 222, 110);
    font-size: 3em;
    width: 3em;
    height: 1.6em;
    display: inline-block;
    text-align: center;
    margin: 0.2em;
}
.leader {
    color: rgb(255, 255, 255);
    font-size: 4em;

}
p {
    text-align: center;
}
</style>