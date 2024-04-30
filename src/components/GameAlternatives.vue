<script setup>
import { ref } from 'vue'
const emit = defineEmits(['user-choice', 'computer-choice', 'winner', 'win-item']) // Definiera 'emit' för att sända händelser.
const alternatives = ref(['scissors', 'paper', 'rock',]) // skapar listan med alternativen

//
function alternativeChosen(e) { //funktion för vald symbol
    let buttons = document.getElementsByClassName('button')
    for (let b of buttons) {
        b.classList.remove('vald')
    }
    let alternative = e.target.id //hämtar ID på den valda symbolen
    e.target.classList.add('vald')// sätter klassen "vald" på symbol som klickats på
    emit('user-choice', alternative)//skickar ut användarens val
    computerAction()//anropar funktionen för att få dators val
}

function computerAction() { // har datorn att välja symbol
    let compAlternative = alternatives.value[Math.floor(Math.random() * alternatives.value.length)] // väljer slumpmässigt ett val för dator
    let buttons = document.getElementsByClassName('button') 
    for (let b of buttons) {
        b.classList.remove('computerChoice')
    }
    document.getElementById(compAlternative).classList.add('computerChoice')// ger det som datorn valt klassen "computerChoice"
    emit('computer-choice', compAlternative)
    determineWinner()//anropar funktion för att räkna ut vem som vann
}
function determineWinner() { //funktion för att avgöra vinnare
    let userButton, computerButton 
    let buttons = document.getElementsByClassName('button')
    for (let b of buttons) {
        if (b.classList.contains('vald')) {
            userButton = b.id // om knappen är vald sparas ID för användarens valda knapp
        }
        if (b.classList.contains('computerChoice')) {
            computerButton = b.id// om knappen är vald sparas ID för datorns valda knapp
        }
    }
    let computerIndex = alternatives.value.indexOf(computerButton)
    let userIndex = alternatives.value.indexOf(userButton)
    if (computerButton === userButton) { //om dator och användare väljer samma 
        emit('winner', 'draw') // visa oavgjorthändelse
    } else if (computerIndex % 2 === userIndex % 2) {
        emit('winner', computerIndex > userIndex ? 'computer' : 'user')//visar vem som vann
        emit('win-item', computerIndex > userIndex ? computerButton : userButton) // visar vilket "objekt som vann, tex sax."
    } else {
        emit('winner', computerIndex < userIndex ? 'computer' : 'user')
        emit('win-item', computerIndex < userIndex ? computerButton : userButton)
    }
}

</script>

<template>

    <ul> <!-- Lista för att visa alternativen. -->
        <li v-for="alt of alternatives" @click="alternativeChosen" :key="alt" :id="alt" class="button"> <!-- Skapar  knapp för varje alternativ. -->
            <img :src="`src/assets/${alt}.png`" style="height: 2rem;" class="ignore" /> <!-- Visar bild för varje alternativ. -->
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