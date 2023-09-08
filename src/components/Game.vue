<template>
    <div class="game-container">
      <div class="player-choice">
        <img :src="playerImgUrl" />
        <p>{{ playerChoice }}</p>
      </div>
      <div class="vs-divider">VS</div>
      <div class="computer-choice">
        <img :src="computerImgUrl" />
        <p>{{ computerChoice }}</p>
      </div>
      <div class="scoreboard">
        <button class="bottom-button" @click="randomChoice">เป้า ยิ้ง ฉุบ</button>
        <h3>คะแนน</h3>
        <p>{{ playerScore }} : {{ computerScore }}</p>
      </div>
      <button class="bottom-button" @click="resetGame">เริ่มใหม่</button>
    </div>
  </template>
  
  <script>
  import { ref } from 'vue'
  
  const imgUrl = ref(new URL('./assets/default.png', import.meta.url).href)
  const choices = ['rock', 'paper', 'scissors', 'heart']
  
  export default {
    setup() {
      const playerImgUrl = ref('')
      const computerImgUrl = ref('')
      const playerChoice = ref('')
      const computerChoice = ref('')
      const playerScore = ref(0)
      const computerScore = ref(0)
  
      function randomChoice() {
        playerChoice.value = choices[Math.floor(Math.random() * choices.length)]
        computerChoice.value = choices[Math.floor(Math.random() * choices.length)]
  
        playerImgUrl.value = new URL(`./assets/${playerChoice.value}.png`, import.meta.url).href
        computerImgUrl.value = new URL(`./assets/${computerChoice.value}.png`, import.meta.url).href
  
        determineWinner()
      }
  
      function determineWinner() {
        if (playerChoice.value === computerChoice.value) {
          // ไม่มีคะแนนเพิ่มขึ้น
        } else if (
          (playerChoice.value === 'rock' && computerChoice.value === 'scissors') ||
          (playerChoice.value === 'paper' && computerChoice.value === 'rock') ||
          (playerChoice.value === 'scissors' && computerChoice.value === 'paper') ||
          (playerChoice.value === 'heart')
        ) {
          playerScore.value++
        } else {
          computerScore.value++
        }
      }
  
      function resetGame() {
        playerScore.value = 0
        computerScore.value = 0
        playerImgUrl.value = new URL('./assets/default.png', import.meta.url).href
        computerImgUrl.value = new URL('./assets/default.png', import.meta.url).href
        playerChoice.value = ''
        computerChoice.value = ''
      }
  
      return {
        playerImgUrl,
        computerImgUrl,
        playerChoice,
        computerChoice,
        playerScore,
        computerScore,
        randomChoice,
        resetGame
      }
    }
  }
  </script>
  
  <style scoped>
  .game-container {
    text-align: center;
  }
  
  .player-choice,
  .computer-choice {
    display: inline-block;
    margin: 20px;
  }
  
  img {
    max-width: 100px;
  }
  
  .button-wrapper button,
  .scoreboard p {
    margin: 5px;
  }


    .vs-divider {
    font-size: 20px;
    margin: 0 10px;
    }


  .bottom-button {
    margin-top: 10px;
    padding: 10px 20px;
    font-size: 14px;
    background-color: #4caf50;
    color: #ffffff;
    border: none;
    cursor: pointer;
    border-radius: 5px;
    transition: background-color 0.3s;
  }

  .bottom-button:hover {
    background-color: #45a049;
  }
  </style>
  