<template>
  <div id="app" class="container">
    <div class="row">
      <div class="col-md-12 col-md-12 controls shadow p-3 mb-5 bg-white rounded">
        <div class="row">
          <div class="col-md-1"></div>
          <div class="col-md-5 ">
            <h1>You</h1>
            <div class="progress">
              <div class="progress-bar" 
                  :style="{width:playerHealth+'%'}">
                    {{playerHealth}}
              </div>
            </div>  
          </div>
          <div  class="col-md-5 ">
            <h1>Opponent</h1>
            <div class="progress">
              <div class="progress-bar" 
                  :style="{width:monsterHealth+'%'}">
                    {{monsterHealth}}
              </div>
            </div>
          </div>
          <div class="col-md-1"></div>
        </div>
      </div>
      <div class="col-md-12 controls shadow p-3 mb-5 bg-white rounded" v-if="!gameIsRunning">
          <button class="btn btn-lg btn-success float-center" @click="startGame">
            Start New Game
          </button>
      </div>
      <div class="col-md-12 controls shadow p-3 mb-5 bg-white rounded" v-else>
        <button class="btn btn-lg btn-danger float-center btn-space" @click="attack">
          Attack
        </button>
        <button class="btn btn-lg btn-warning float-center btn-space" @click="specialAttack">
          Special Attack
        </button>
        <button class="btn btn-lg btn-primary float-center btn-space" @click="heal">
          Heal
        </button>
        <button class="btn btn-lg float-center btn-space" @click="giveUp">
          Give Up
        </button>
      </div>
      <section class="row log" v-if="turns.length>0">
        <div class="col-md-12 controls">
          <ul>
            <li v-for="(turn,index) in turns" :key="index">
              {{turn.text}}
            </li>
          </ul>
        </div>
      </section>
    </div>
  </div>
</template>

<script>
export default {
  name: 'app',
  data () {
    return {
      playerHealth:100,
      monsterHealth:100,
      gameIsRunning: false,
      turns: []
    }
  },
  methods: {
    startGame () {
      this.gameIsRunning =  true
      this.playerHealth = 100
      this.monsterHealth = 100
      this.turns = []
    },
    attack () { 
      let damage =  this.calculateDamage(3,10)
      this.monsterHealth -= damage
      if(this.checkWin()){
        return
      }
      this.turns.unshift({
        isPlayer : true,
        text:'The player hits monster by' + damage
      })

      this.monsterAttacks()
    },
    specialAttack () {
      this.monsterHealth -= this.calculateDamage(10,20)
      if(this.checkWin()){
        return
      }

      this.monsterAttacks()

    },
    heal () {
      if(this.playerHealth<=90){
        this.playerHealth += 10
      } else {
        this.playerHealth = 100
      }
      this.monsterAttacks()
    },
    giveUp () {
      this.gameIsRunning = false
    },
    calculateDamage(min,max){
      return Math.max(Math.floor(Math.random() * max), min)
    },
    checkWin(){
      if(this.monsterHealth<=0){
        if(confirm('You Won. New Game?')){
          this.startGame()
        } else {
          this.gameIsRunning = false
        }
        return true
      } else if(this.playerHealth<=0) {
          if(confirm('You Lost. New Game?')){
            this.startGame()
          } else {
            this.gameIsRunning = false
          }
          return true
      }
      return false
    },
    monsterAttacks(){
      let damage = this.calculateDamage(5,12)
      this.playerHealth -= damage
      this.turns.unshift({
        isPlayer : false,
        text:'The Monster hits Player by' + damage
      })
      this.checkWin()
    }
  }
}
</script>

<style>
.controls{
  text-align: center;
}
.btn-space {
    margin-right: 25px;
}
/*
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.row{
  margin: 2%;
}

h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
*/
ul {
  list-style-type: none;
    font-size: 20px;
}
li {
  margin: auto;
  padding: 3px;
  text-align: left;
}

.progress{
  height: 40px;
}
</style>
