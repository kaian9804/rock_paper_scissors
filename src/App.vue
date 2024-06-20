l<!-- sources: https://github.com/stevenlei/assets-scissor-rock-paper -->
<!-- ppt: https://slides.com/stevenlei/cm521-06-2024-c-004?token=H_GvStbk#/1/1 -->

<template>
  <h1>Rock Paper Scissors!</h1>

  <div id="container">
    <div id="bot_placeholder">
      <img v-bind:src="bot_img" alt="Placeholder-Bot" class="placeholder">
    </div>

    <div id="me_placeholder">
      <img v-bind:src="my_img" alt="Placeholder-You" class="placeholder">
    </div>

    <div id="btn_container">
      <div id="btn_paper" @click="() => picking(1)"></div>
      <div id="btn_scissor" @click="() => picking(2)"></div>
      <div id="btn_rock" @click="() => picking(3)"></div>
    </div>
  </div>

  <p>Number of My Winnings: {{ i_win }}</p>
  <p>Number of Bot's Winnings: {{ bot_wins }}</p>
  <p>Number of DRAW: {{ draw }}</p>

  <button @click="() => restart()">RESTART</button>

  <p id="creator">Created by Ka Ian @ 2024</p>

</template>

<script>

export default {
  name: 'App',
  data() {
    return {
      my_id: 414,
      bot_img: '/images/Placeholder-Bot.png',
      my_img: '/images/Placeholder-You.png',
      i_win: 0,
      bot_wins: 0,
      draw: 0,
    }
  },
  methods: {
    picking(my_choice) {

      // my picking
      console.log(`my_choice: ${my_choice}`)
      var my_meaning = "my_meaning";

      if (my_choice == 1) {
        my_meaning = 'paper';
      } else if (my_choice == 2) {
        my_meaning = 'scissor';
      } else if (my_choice == 3) {
        my_meaning = 'rock';
      } else {
        console.log('ERROR in My Picking');
      }

      // random bot_choice
      let bot_choice = Math.floor(Math.random()*3)+1;
      var bot_meaning = "bot_meaning";

      console.log(`bot_choice: ${bot_choice}`);
      if (bot_choice == 1) {
        bot_meaning = 'paper';
      } else if (bot_choice == 2) {
        bot_meaning = 'scissor';
      } else if (bot_choice == 3) {
        bot_meaning = 'rock';
      } else {
        console.log('ERROR in Bot Picking');
      }

      // win or lost
      let my_result = 'my_result';
      let bot_result = 'my_result';
      if (my_choice == bot_choice) {
        my_result = 'draw';
        bot_result = 'draw';
      } else if (my_choice == 1) {
        if (bot_choice == 2) {
          my_result = 'lose';
          bot_result = 'win';
        } else if (bot_choice == 3) { 
          my_result = 'win';
          bot_result = 'lose';
        }
      } else if (my_choice == 2) {
        if (bot_choice == 1) {
          my_result = 'win';
          bot_result = 'lose';
        } else if (bot_choice == 3) {
          my_result = 'lose';
          bot_result = 'win';
        }
      } else if (my_choice == 3) {
        if (bot_choice == 1) {
          my_result = 'lose';
          bot_result = 'win';
        } else if (bot_choice == 2) {
          my_result = 'win';
          bot_result = 'lose';
        }
      }

      // construct the path for bot and my img
      this.my_img = `/images/${my_meaning}-${my_result}.png`;
      this.bot_img = `/images/${bot_meaning}-${bot_result}.png`;

      // wins counting
      if (my_result == 'win') {
        this.i_win += 1;
      } else if (bot_result == 'win') {
        this.bot_wins += 1;
      } else {
        this.draw += 1;
      }
    },
    restart() {
      this.i_win = 0;
      this.bot_wins = 0;
    }
  }
}
</script>

<style>
html, body {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  padding: 0;
  margin: 10;
  background-color: #44d7b6;
}

h1 {
  text-align: center;
}

#creator {
  font-size: 10px;
  text-align: center;
}

#container {
  display: flex;
  flex-direction: column;
  width: 100%;
  height: 100%;
  box-sizing: border-box;
}

#bot_placeholder, #me_placeholder {
  flex: 0px 2 1;
  margin: 5px;
}

#bot_placeholder img, #me_placeholder img {
  display: block;
  width: 40%;
  height: auto;
  margin: auto;
}

#btn_container {
  flex: 0px 1 1;
  display: flex;
  flex-direction: row;
}

#btn_container div {
  flex: 0px 1 1;
  background-size: contain;
  background-repeat: no-repeat;
  background-position: center bottom;
  width: 30%;
  height: 80px;
}

#btn_container div#btn_paper {
  background-image: url('/public/images/paper-btn.png');
}

#btn_container div#btn_scissor {
  background-image: url('/public/images/scissor-btn.png');
}

#btn_container div#btn_rock {
  background-image: url('/public/images/rock-btn.png');
}
</style>
