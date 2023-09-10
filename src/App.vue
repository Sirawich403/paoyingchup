<script setup>
import { ref } from 'vue'
</script>

<template>
  <div id="app">
    <div class="borderr">
      <div class="game-container">
        <div class="team">
          <h2>TeamA</h2>
              <img  v-if="teamAChoice ===''" src="/src/assets/rock.png" alt="Rock">
              <img  v-if="teamAChoice ==='Rock'" :src="'/src/assets/rock.png'" alt="Rock">
              <img  v-if="teamAChoice ==='Paper'" src="/src/assets/paper.png" alt="Paper">      
              <img  v-if="teamAChoice ==='Scissors'" src="/src/assets/sci.png" alt="Scissors">
              <img  v-if="teamAChoice ==='Luv'" src="/src/assets/loveeee.png" alt="Luv">
        </div>
        <div class="team">
          <h2>TeamB</h2>
          <img  v-if="teamAChoice ===''" src="/src/assets/rock.png" alt="Rock">
              <img  v-if="teamBChoice ==='Rock'" src="/src/assets/rock.png" alt="Rock">
              <img  v-if="teamBChoice ==='Paper'" src="/src/assets/paper.png" alt="Paper">      
              <img  v-if="teamBChoice ==='Scissors'" src="/src/assets/sci.png" alt="Scissors">
              <img  v-if="teamBChoice ==='Luv'" src="/src/assets/loveeee.png" alt="Luv">
        </div>
        <div class="score">
          <p>{{ scoreOutput }}</p>
        </div>
        <div class="result">
          <p>{{ gameResult }}</p>
        </div>
        <div class="buttons">
          <button id="playy" class="play" @click="playGame">Play</button>
          <button id="reset" class="play" @click="resetGame">Reset</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      choices: ['Rock', 'Paper', 'Scissors', 'Luv'],
      teamAChoice: '',
      teamBChoice: '',
      scoreTeamA: 0,
      scoreTeamB: 0,
      gameResult: '',
    };
  },
  computed: {
    scoreOutput() {
      return `Team A : ${this.scoreTeamA} - Team B ${this.scoreTeamB}`;
    },
  },
  methods: {
    getRandomChoice() {
      return this.choices[Math.floor(Math.random() * this.choices.length)];
    },
    determineWinner(choiceA, choiceB) {
      if (choiceA === choiceB) {
        return 'Tie';
      } else if (choiceA === 'Luv') {
        return 'TeamA';
      } else if (choiceB === 'Luv') {
        return 'TeamB';
      } else if (
        (choiceA === 'Rock' && choiceB === 'Scissors') ||
        (choiceA === 'Paper' && choiceB === 'Rock') ||
        (choiceA === 'Scissors' && choiceB === 'Paper')
      ) {
        return 'TeamA';
      } else {
        return 'TeamB';
      }
    },
    playGame() {
      this.teamAChoice = this.getRandomChoice();
      this.teamBChoice = this.getRandomChoice();
      const winner = this.determineWinner(this.teamAChoice, this.teamBChoice);

      if (winner === 'TeamA') {
        this.scoreTeamA++;
        this.gameResult = 'Team A Win!!';
      } else if (winner === 'TeamB') {
        this.scoreTeamB++;
        this.gameResult = 'Team B Win!!';
      } else {
        this.gameResult = 'Tie';
      }
    },
    resetGame() {
      this.teamAChoice = '';
      this.teamBChoice = '';
      this.scoreTeamA = 0;
      this.scoreTeamB = 0;
      this.gameResult = '';
    },
    getImageSrc(choice) {
      return choice ? `images/${choice.toLowerCase()}.png` : '';
    },
  },
};
</script>

<style scoped>
body {
  background-color: #007bff; /* Change background color to blue */
  color: #fff6f6; /* Change font color to white */
  font-family: "Arial", sans-serif;
}

.borderr {
  margin-top: 2%;
 
  background-color: #c5f5f8;
  width: 70vw;
  max-height: 80%;
  border-radius: 20px;
}

/* Center align the game container */
.game-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  width: 100%;
}

/* Style other elements as needed */
.team {
  text-align: center;
  margin: 20px;
}

img {
  width: 100px;
  height: 100px;
}

.score {
  margin: 20px;
}

.result {
  margin: 20px;
}

#playy {
  margin-right: 15px;
}

#reset {
  margin-left: 15px;
}

.play {
  margin-bottom: 20px;
  display: inline-block;
  outline: none;
  cursor: pointer;
  font-size: 14px;
  line-height: 1;
  border-radius: 500px;
  transition-property: background-color, border-color, color, box-shadow, filter;
  transition-duration: 0.3s;
  border: 1px solid transparent;
  letter-spacing: 2px;
  min-width: 140px;
  text-transform: uppercase;
  white-space: normal;
  font-weight: 700;
  text-align: center;
  font-family: "Arial", serif;
  padding: 17px 48px;
  color: #007bff; /* Change button font color to blue */
  background-color: #f8f295;
  height: 48px;
}

.play:hover {
  transform: scale(1.04);
  background-color: #8bc1ff;
}
</style>

