<template>
  <header>
    <h1>Monster Slayer</h1>
  </header>
  <div id="game">
    <section id="monster" class="container">
      <h2>Monster Health</h2>
      <div class="healthbar">
        <div
          class="healthbar__value"
          :style="{ width: monsterHealth <= 0 ? '0%' : monsterHealth + '%' }"
        ></div>
      </div>
    </section>
    <section id="player" class="container">
      <h2>Your Health</h2>
      <div class="healthbar">
        <div
          class="healthbar__value"
          :style="{ width: playerHealth <= 0 ? '0%' : playerHealth + '%' }"
        ></div>
      </div>
    </section>
    <section class="gameover" v-if="winner">
        <h2>Game Over!</h2>
      <h2 v-if="winner === 'player'">You Won!</h2>
      <h2 v-else-if="winner === 'tie'">Game Tie!</h2>
      <h2 v-else-if="winner === 'monster'">Monster Won!</h2>
      <button @click="startNewGame">Start New Game!</button>
    </section>
    <section v-if="!winner" id="controls">
      <button @click="attackOnMonster">ATTACK</button>
      <button @click="specialAttackOnMonster" :disabled="mayUseSpecialAttack">
        SPECIAL ATTACK
      </button>
      <button @click="healPlayer">HEAL</button>
      <button @click="surrender">SURRENDER</button>
    </section>
    <section id="log" class="container">
      <h2>Battle Log</h2>
      <ul>
        <li v-for="(message,index) in logMessages" :key='index'>{{ logMessages.length - index }}) {{ message.who }} - {{ message.what }} - {{ message.value }}</li>
      </ul>
    </section>
  </div>
  <br />
  <br />
  <br />
  <br />
  <br />
  <br />
</template>

<script>
const getRandomValue = (min, max) => {
  return Math.floor(Math.random() * (max - min)) + min;
};
export default {
  name: "MonsterSlayer",
  data() {
    return {
      playerHealth: 100,
      monsterHealth: 100,
      currentRound: 0,
      winner: null,
      logMessages:[],
      // specialAttackEnabled:false
    };
  },
  methods: {
    attackOnMonster() {
      const attackValue = getRandomValue(5, 12);
      this.monsterHealth -= attackValue;
      this.attackOnPlayer();
      this.currentRound += 1;
      this.logMessages.unshift({who:"player",what:"attack",value:attackValue})
    //   console.log(this.logMessages)
      // console.log(this.currentRound)
    },
    attackOnPlayer() {
      const attackValue = getRandomValue(8, 15);
      this.playerHealth -= attackValue;
      this.logMessages.unshift({who:"monster",what:"attack",value:attackValue})

    },
    specialAttackOnMonster() {
      const attackValue = getRandomValue(10, 25);
      this.monsterHealth -= attackValue;
      this.attackOnPlayer();
      this.currentRound = 0;
      this.logMessages.unshift({who:"player",what:"special attack",value:attackValue})
    },
    healPlayer() {
      this.currentRound++;
      const healValue = getRandomValue(8, 20);
      if (this.playerHealth + healValue > 100) this.playerHealth = 100;
      else this.playerHealth += healValue;
      this.attackOnPlayer();
      this.logMessages.unshift({who:"player",what:"heal",value:healValue})
    },
    startNewGame(){
        this.playerHealth= 100
        this.monsterHealth= 100
        this.currentRound= 0
        this.winner= null
        this.logMessages=[]
    },

    surrender(){
        this.winner="monster"
      this.logMessages.unshift({who:"player",what:"surrendered",value:'lost'})
    }
  },
  computed: {
    mayUseSpecialAttack() {
      if (this.currentRound < 3) return true;
      return false;
    },
  },

  watch: {
    playerHealth(value) {
      if (value <= 0 && this.monsterHealth <= 0) {
        //draw
        this.winner = "tie";
      } else if (value <= 0) {
        //monster win
        this.winner = "monster";
      }
    },
    monsterHealth(value) {
      if (value <= 0 && this.playerHealth <= 0) {
        //draw
      } else if (value <= 0) {
        //player win
        this.winner = "player";
      }
    },
  },
};
</script>

<style scoped>
* {
  box-sizing: border-box;
}

html {
  font-family: "Jost", sans-serif;
}

body {
  margin: 0;
}

header {
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
  padding: 0.5rem;
  background-color: #880017;
  color: white;
  text-align: center;
  margin-bottom: 2rem;
}

section {
  width: 90%;
  max-width: 40rem;
  margin: auto;
}

.healthbar {
  width: 100%;
  height: 40px;
  border: 1px solid #575757;
  margin: 1rem 0;
  background: #fde5e5;
}

.healthbar__value {
  background-color: #00a876;
  width: 100%;
  height: 100%;
}

.container {
  text-align: center;
  padding: 0.5rem;
  margin: 1rem auto;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
  border-radius: 12px;
}

#monster h2,
#player h2 {
  margin: 0.25rem;
}

#controls {
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  align-items: center;
  justify-content: center;
}

button {
  font: inherit;
  border: 1px solid #88005b;
  background-color: #88005b;
  color: white;
  padding: 1rem 2rem;
  border-radius: 12px;
  margin: 1rem;
  width: 12rem;
  cursor: pointer;
  box-shadow: 1px 1px 4px rgba(0, 0, 0, 0.26);
}

button:focus {
  outline: none;
}

button:hover,
button:active {
  background-color: #af0a78;
  border-color: #af0a78;
  box-shadow: 1px 1px 8px rgba(0, 0, 0, 0.26);
}

button:disabled {
  background-color: #ccc;
  border-color: #ccc;
  box-shadow: none;
  color: #3f3f3f;
  cursor: not-allowed;
}

#log ul {
  list-style: none;
  margin: 0;
  padding: 0;
}

#log li {
  margin: 0.5rem 0;
}

.log--player {
  color: #7700ff;
}

.log--monster {
  color: #da8d00;
}

.log--damage {
  color: red;
}

.log--heal {
  color: green;
}
.gameover {
  text-align: center;
  border: 2px solid rgba(0, 0, 0, 0.189);
  box-shadow: 3px 0px 5px 7px rgba(0, 0, 0, 0.34);
  -webkit-box-shadow: 3px 0px 5px 7px rgba(0, 0, 0, 0.34);
  -moz-box-shadow: 3px 0px 5px 7px rgba(0, 0, 0, 0.34);
}
</style>
