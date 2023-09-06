<template>
  <div id="app">
    <h1 class="title">Rock, Paper, Scissors and Love Game</h1>

    <div class="players">
      <div class="player">
        <h2>You</h2>
        <p class="score">Score: {{ userScore }}</p>
        <div class="choice">
          <img v-if="userChoice === 'rock.png'" src="https://furringline.com/wp-content/uploads/2019/11/equipments-meta-electrician-hammer-300g-1-1500x1500.jpg" alt="Rock" />
          <img v-if="userChoice === 'paper.png'" src="https://555paperplus.com/media/catalog/product/cache/5/image/1800x/040ec09b1e35df139433887a97daa66f/l/t/lta4-at-wh_pic1.jpg" alt="Paper" />
          <img v-if="userChoice === 'scissors.png'" src="https://www.doodeebox.com/wp-content/uploads/2022/04/scissor.jpg" alt="Scissors" />
          <img v-if="userChoice === 'love.png'" src="https://s.isanook.com/ca/0/ud/282/1414083/red-heart_2764-fe0f.png?ip/resize/w728/q80/png" alt="love" />
        </div>
      </div>

      <div class="computer">
        <h2>Computer</h2>
        <p class="score">Score: {{ computerScore }}</p>
        <div class="choice">
          <img v-if="computerChoice === 'rock.png'" src="https://furringline.com/wp-content/uploads/2019/11/equipments-meta-electrician-hammer-300g-1-1500x1500.jpg" alt="Rock" />
          <img v-if="computerChoice === 'paper.png'" src="https://555paperplus.com/media/catalog/product/cache/5/image/1800x/040ec09b1e35df139433887a97daa66f/l/t/lta4-at-wh_pic1.jpg" alt="Paper" />
          <img v-if="computerChoice === 'scissors.png'" src="https://www.doodeebox.com/wp-content/uploads/2022/04/scissor.jpg" alt="Scissors" />
          <img v-if="computerChoice === 'love.png'" src="https://s.isanook.com/ca/0/ud/282/1414083/red-heart_2764-fe0f.png?ip/resize/w728/q80/png" alt="love" />
        </div>
      </div>
    </div>

    <div class="choices">
      <button @click="playRandom" class="play-random-button">Play</button>
    </div>

    <div class="result">
      <button @click="resetGame" class="reset-button">Play Again</button>
      <p class="result-message">{{ resultMessage }}</p>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      userScore: 0,
      computerScore: 0,
      resultMessage: '',
      userChoice: '',
      computerChoice: '',
    };
  },
  methods: {
    play(userChoice) {
      const choices = ['rock.png', 'paper.png', 'scissors.png', 'love.png']; // เพิ่ม "ความรัก" ในตัวเลือก

      const userChoiceIndex = choices.indexOf(userChoice);
      const computerChoiceIndex = Math.floor(Math.random() * choices.length);

      const computerChoice = choices[computerChoiceIndex];

      const userChoiceImage = userChoice;
      const computerChoiceImage = computerChoice;

      this.userChoice = userChoiceImage;
      this.computerChoice = computerChoiceImage;

      if (userChoice === computerChoice) {
        this.resultMessage = "It's a tie!";
      } else if (
        (userChoice === 'rock.png' && computerChoice === 'scissors.png') ||
        (userChoice === 'paper.png' && computerChoice === 'rock.png') ||
        (userChoice === 'scissors.png' && computerChoice === 'paper.png') ||
        (userChoice === 'love.png') // ความรักชนะทุกครั้ง
      ) {
        this.resultMessage = 'You win!';
        this.userScore++;
      } else {
        this.resultMessage = 'Computer wins!';
        this.computerScore++;
      }
    },
    resetGame() {
      this.userScore = 0;
      this.computerScore = 0;
      this.resultMessage = '';
      this.userChoice = '';
      this.computerChoice = '';
    },
    playRandom() {
      const choices = ['rock.png', 'paper.png', 'scissors.png', 'love.png']; // เพิ่ม "ความรัก" ในตัวเลือก
      const userChoiceIndex = Math.floor(Math.random() * choices.length);
      const userChoice = choices[userChoiceIndex];
      this.play(userChoice);
    },
  },
};
</script>




<style scoped>
#app {
  font-family: Arial, sans-serif;
  text-align: center;
  padding: 10px;
  background-color: #ffffff;
  color: #000000;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  height: 100vh; /* ทำให้เต็มหน้าจอ */
  width: 100vh;
}

.title {
  font-size: 36px;
  margin-top: 0px;
  color: #000000; /* สีข้อความเข้ม */
}
.choice img {
  width: 150px; /* กำหนดความกว้างของรูปภาพ */
  height: 150px; /* กำหนดความสูงของรูปภาพ */
}
.players {
  display: flex;
  justify-content: space-around;
  margin-top: 20px;
  width: 100%;
  margin-bottom: 40px;
}

.player,
.computer {
  text-align: center;
  background-color: #ffffff;
  color: #000000;
  border-radius: 8px;
  padding: 20px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  width: 45%; /* ปรับความกว้างของส่วนของผู้เล่นและคอมพิวเตอร์ */
}

.score {
  font-size: 24px;
  margin-bottom: 10px;
}

.choices {
  display: flex;
  justify-content: space-around;
}

button {
  font-size: 18px;
  padding: 10px 20px;
  margin: 5px;
  cursor: pointer;
  background-color: #000000;
  color: #ffffff;
  border: none;
  border-radius: 4px;
  transition: background-color 0.3s ease;
}

button:hover {
  background-color: #333333;
}

.result {
  margin-top: 20px;
}

.result-message {
  font-size: 24px;
  font-weight: bold;
  margin-bottom: 10px;
}

.reset-button {
  font-size: 18px;
  padding: 10px 20px;
  background-color: #000000;
  color: #ffffff;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.reset-button:hover {
  background-color: #333333;
}

.play-button {
  margin-top: 20px;
}

.play-random-button {
  font-size: 24px;
  padding: 10px 20px;
  background-color: #000000;
  color: #ffffff;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.play-random-button:hover {
  background-color: #333333;
}
.result-button-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-top: 20px;
}
</style>
