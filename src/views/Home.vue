<template>
  <div class="home">
 <div class="header-container">
        <h1>Elemental Battle</h1>
      </div>
 <div class="container">
   <div class="row">
     <div class="col-lg-6">
 <div id="p-choice">
      <Player v-on:getChoice="updatePlayerChoice($event)" v-bind:choice="player_choice" />
      <h2 style="color:black; text-align:center">You chose: {{player_choice}}</h2>
    </div>
     </div>
     <div class="col-lg-6">
 <div id="o-choice">
      <img type="button" class="quest" v-if="!opponent_choice" src="../assets/quest.png" /> 
      <img class="opponent_img" type="button" v-if="!!opponent_choice" :src="require('../assets/'+ImgSrc())" />
      <h2 style="color:black; text-align:center">Opponents choice: {{opponent_choice}}</h2>
    </div>
     </div>
   </div>
 </div>
    

      <!-- Game -->
   

   
          <Opponent @click="play" v-on:getChoice="updateOpponentScore($event)" v-bind:choice="opponent_choice"/>
    <h1 class="winner" v-if="winner">
      {{ winner }}
    </h1>

  <!-- ScoreBoard -->
      <div class="scoreboard">
      <h2 class="score_text">ScoreBoard</h2>
        <div class="score">
          <h3>YOU : {{player_score}}</h3>
          <h3>OPP : {{opponent_score}}</h3>
      </div>
      </div>
  </div>
      
 
</template>

<script>
import Player from '../components/Player.vue'
import Opponent from '../components/Opponent.vue'

const choices = ["grass", "fire", "water"];
export default {
  name: 'App',
  components: {
    Player,
    Opponent,
  },
  data() {
    return {
      player_choice: "",
      opponent_choice: "",
      player_score: 0,
      opponent_score: 0,
      winner: ""
    };
  },
  methods: {
    updatePlayerChoice(choice) {
        this.player_choice = choice;
      },
    updateOpponentScore(choice) {
        this.opponent_choice = choice;
      }, 
    ImgSrc() {
      if (this.opponent_choice == "grass") {
        return "grass.png"
      }
      else if (this.opponent_choice == "fire") {
        return "fire.png"
      }
      else  {
        return "water.png"
      }
    },
    play() {
      const {player_choice, opponent_choice } = this;
    
    if (player_choice === opponent_choice) {
      this.winner = "It is a tie!";
    } else if (
        (opponent_choice === "water" && player_choice === "fire") ||
         (opponent_choice === "fire" && player_choice === "grass") ||
         (opponent_choice === "grass" && player_choice === "water")
      ) {
          this.opponent_score++;
          this.winner = "Opponent won :(";
    } else if (player_choice === "") {
      alert("You have to select your choice!")
    }
    else {
      this.player_score++;
      this.winner = "You won!";
        }
      }
    }
}
</script>
<style scoped>
.quest{
height: 50px;
}

.header-container {
    background: #fff;
    padding: 25px;
    text-align: center;
}
.header-container>h1 {
  background-color: #fff;
  color: #292c34;
  text-align: center;
  font-family:Cambria, Cochin, Georgia, Times, 'Times New Roman', serif;
}


.score_text {
  background-color: aliceblue;
  text-align: center;
  font-family: 'Roboto Condensed', sans-serif;
  border-bottom: 2px solid #000;
  width:100%;
}


.float-child2 {
  margin-top:200px;
}
h3 {
  background-color: aliceblue;
  text-align: center;
  font-family: 'Do Hyeon', sans-serif;
  font-family: 'Roboto Condensed', sans-serif;
  font-family: 'Source Code Pro', monospace;
}
.score {
  padding: 1rem;
  font-size: 40px;
}
.opponent_img {
  height:150px;
  width: 140px;
  padding-left: 20px;
  border-radius: 10px;
}
.winner {
 text-align: center;
  z-index:2922134;
  padding: 10px;
  border: 5px solid gray;
  margin: 0;
  background-color: gold;
  color:black;
}
</style>