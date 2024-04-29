<script setup>
import { ref } from 'vue'
const emit = defineEmits(['user-choice', 'computer-choice', 'winner', 'win-item'])
const alternatives = ref(['scissors', 'paper', 'rock',])


function alternativeChosen(e) {
    let buttons = document.getElementsByClassName('button')
    for (let b of buttons) {
        b.classList.remove('vald')
    }
    let alternative = e.target.id
    e.target.classList.add('vald')
    emit('user-choice', alternative)
    computerAction()
}

function computerAction() {
    let compAlternative = alternatives.value[Math.floor(Math.random() * alternatives.value.length)]
    let buttons = document.getElementsByClassName('button')
    for (let b of buttons) {
        b.classList.remove('computerChoice')
    }
    document.getElementById(compAlternative).classList.add('computerChoice')
    emit('computer-choice', compAlternative)
    determineWinner()
}
function determineWinner() {
    let userButton, computerButton
    let buttons = document.getElementsByClassName('button')
    for (let b of buttons) {
        if (b.classList.contains('vald')) {
            userButton = b.id
        }
        if (b.classList.contains('computerChoice')) {
            computerButton = b.id
        }
    }
    let computerIndex = alternatives.value.indexOf(computerButton)
    let userIndex = alternatives.value.indexOf(userButton)
    if (computerButton === userButton) {
        emit('winner', 'draw')
    } else if (computerIndex % 2 === userIndex % 2) {
        emit('winner', computerIndex > userIndex ? 'computer' : 'user')
        emit('win-item', computerIndex > userIndex ? computerButton : userButton)
    } else {
        emit('winner', computerIndex < userIndex ? 'computer' : 'user')
        emit('win-item', computerIndex < userIndex ? computerButton : userButton)
    }
}

</script>

<template>

    <ul>
        <li v-for="alt of alternatives" @click="alternativeChosen" :key="alt" :id="alt" class="button">
            <img :src="`src/assets/${alt}.png`" style="height: 2rem;" class="ignore" />
        </li>
    </ul>
</template>

<style scoped>
ul {
    display: flex;
    padding: 0;
    justify-content: center;
}

li {
    list-style-type: none;
    margin: 0.5em;
    background-color: rgb(252, 116, 116);
    padding: 1em;
    border: 2px solid rgb(190, 29, 29);
    border-radius: 0.5em;
}

.vald {
    background-color: rgb(153, 5, 5);
    color: aliceblue;
    font-weight: bold;
}

.computerChoice {
    border: .3em dashed rgb(156, 255, 169)
}

.ignore {
    pointer-events: none;
    user-select: none;
}
</style>