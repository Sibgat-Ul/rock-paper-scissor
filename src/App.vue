<template>
   <div class="gamebody">

      <div class="players" v-if="!ready">
        <p> Name of the player(s): </p>

        <form @submit.prevent="entNam">

            <input class="name" id="name1" name="name" type="text" >
            <!--<span> Vs </span>
            <input class="name" id="name2" name="name" type="text" > -->
            <br>
            <input type="submit" name="name" value="Start">

        </form>

        
        <section v-if="name1">
              <p> Hello {{ name1 }}, and {{ name2 }} </p>
              <p> Are you ready to start your game? </p>
              <button @click="this.ready = true"> Yes </button>
              <button @click="this.ready = false"> No </button>
        </section>

      </div>  

      <Scoreboard :score1='Number(this.fscore1)' :score2='Number(this.sscore2)' v-if='ready' :name1='name1' :name2='name2'/>
      <RockPaperScissor @score-update='setScore' @new-game='setScore' v-if="ready" :name1='name1' :name2='name2'/>

     <!-- <div class="game" v-if="ready">
          <RockPaperScissor :name1="name1" :name2="name2"/>
      </div>     -->

   </div>    
</template>

<script>

import RockPaperScissor from './components/RockPaperScissor.vue'
import Scoreboard from './components/scoreboard.vue'

export default {
  name: 'App',
  components: {
    RockPaperScissor,
    Scoreboard
  },
  data() {
    return {
      name1: '',
      name2: 'Comp',
      ready: false,
      fscore1: '',
      sscore2: '',
      declare: false,

    }
  },
  methods: {
    entNam() {
      let firstName = document.getElementById('name1').value
    //  let secondName = document.getElementById('name2').value

      if( firstName /* && secondName */ ) {
        this.name1 = document.getElementById('name1').value
      //  this.name2 = document.getElementById('name2').value
      }

      document.getElementById('name1').value = ''
    //  document.getElementById('name2').value = ''

    },

    setScore(fscore, sscore) {
      this.fscore1 = fscore
      this.sscore2 = sscore
    }
  }
}
</script>

<style>
@import url('./../../fontawesome-free-5.14.0-web/css/all.css');

* {
  margin: 0;
  padding: 0;
  font-family: 'Gill Sans', 'Gill Sans MT', Calibri, 'Trebuchet MS', sans-serif;
  scroll-behavior: smooth;
}

#app {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

html {
  height: 100%;
  background-color: #2167a0;
  color:white;
  margin: 0;
}

.gamebody .players{
  font-size: 27px;
  color: white;
}

form {
  display: flex;
  flex-direction: column;
  flex-wrap: nowrap;
  align-items: center;
  align-self: center;
}

input{
  display: block;
  width: 300px;
  height: 40px;
  outline: none;
  border-radius: 8px;
  font-size: 23px;
  font-family: inherit;
  margin: 20px;
}

button {
  display: inline-block;
  width: 300px;
  height: 40px;
  outline: none;
  border-radius: 8px;
  font-size: 23px;
  font-family: inherit;
  margin: 20px;
}

.game {
  font-size: 27px;
  color: white;
}

.scoreboard {
  margin: 20px;
}
</style>
