<template>

  <div class="hello">

    <h3 v-if="!(this.score1 == 3 || this.score2 == 3)"> Let's Begin </h3>

    <div id="gameWindow" v-if="!(this.score1 == 3 || this.score2 == 3)">

      <div class="game Player1">

        <h3> 
          {{ name1 }} 
        </h3> 

       <!-- <span> 
            <i v-for="(item, index) in items" :key="index" @click="winUser(index)" :id="`userstar ${index}`" class="far fa-star"></i> 
        </span> -->

        <p>
            <span v-for="(item, index) in items" :key="index">
              <i @click="startGame(item.name)"  id="fas-target1" :class="item.class" ></i>
            </span>
        </p>  

      </div>

      <div class="game Player2">

        <h3>
          {{ name2 }}
        </h3>
        
      <!--  <span>
          <i v-for="(item, index) in items" :key="index" @click="winUser2(index)" :id="`user2star ${index}`" class="far fa-star"></i>
        </span> -->

        <p id="comp">
          <span class="excess" v-if='!started'> Choosing.... </span>
          <i id='fas-target2'></i>
        </p>  

      </div>
      
    </div>  

    <div class="btncont">
      <button id="newGame" @click="newGame" :disabled='!disable'> New game </button>
    </div>

  </div>

</template>

<script>
export default {
  name: 'RockPaperScissor',
  props: {
    name1: {
        type: String,
        default: 'User'
      },
    name2: {
        type: String,
        default: 'Comp'
      }
  },
  data() {
    return {
      items: [
        {
          name: 'Rock',
          class:'fas fa-hand-rock'
        },
        {
          name: 'Paper',
          class:'fas fa-file-alt'
        },
        {
          name: 'Scissor',
          class:'fas fa-cut'
        }
      ],
      started: false,
      gameCounter: 0,
      disable: false,
      fplayerClass: ' ',
      splayerClass: ' ',
      fitem: ' ',
      sitem: ' ',
      score1: 0,
      score2: 0,
      star1: 0,
      star2: 0,
      win1: false,
      win2: false
    }
  },
  methods: {
    winUser(index) {
      var target = document.getElementById(`userstar ${index}`)
      target.className = "fas fa-star";
      this.star1++
      //this.fplayerClass = this.items[index].name
    },

    winUser2(index) {
      var target = document.getElementById(`user2star ${index}`)
      target.className = "fas fa-star";
      this.star2++
    },

    startGame(itemname) {
      let target2 = document.getElementById('fas-target2')
      let rand2 = Math.round(Math.random() * 2)
      let item2 = this.items[rand2]

      this.fitem = itemname
      this.sitem = item2.name

      this.started = true
      
      target2.className = item2.class

      this.gameCounter++
      
      if(this.gameCounter == 3) {
        this.disable = true
      }
      

    if((this.fitem == 'Rock' && this.sitem == 'Scissor') || (this.fitem == 'Scissor' && this.sitem == 'Rock'))
    {

      (this.fitem == 'Rock' && this.sitem == 'Scissor')?  this.score1++ : this.score2++

      this.$emit('score-update', this.score1, this.score2)

    } 
    
    else if((this.fitem == 'Scissor' && this.sitem == 'Paper') || (this.fitem == 'Paper' && this.sitem == 'Scissor'))
    {
        
      (this.fitem == 'Scissor' && this.sitem == 'Paper')?  this.score1++ : this.score2++

      this.$emit('score-update', this.score1, this.score2)
       
    } 
    
    else if((this.fitem == 'Paper' && this.sitem == 'Rock') || (this.fitem == 'Rock' && this.sitem == 'Paper'))
    {
        
      (this.fitem == 'Paper' && this.sitem == 'Rock')?  this.score1++ : this.score2++

      this.$emit('score-update', this.score1, this.score2)

    }

    else ('draw')

    this.$emit('score-update', this.score1, this.score2)
 
    },

    newGame() {
      this.started = false
      this.disable = false

      this.gameCounter = 0
      this.score1 = 0
      this.score2 = 0

      this.$emit('new-game', this.score1, this.score2)
    }

  }
}
</script>

<!-- star icon: <i class="fas fa-star"></i> -->
<style scoped>

* {
  color: #ffffff;
  font-family: 'Gill Sans', 'Gill Sans MT', Calibri, 'Trebuchet MS', sans-serif;
  text-align: center;
}

.hello h3 {
  font-size: 40px;
  margin: 10px;
}

.game h3 {
  margin: 10px;
}

#gameWindow {
  display: grid;
  grid-template-columns: 1fr 1fr;
  font-size: 48px;
  width: 80%;
  margin: auto;
}

#gameWindow .game {
  font-size: 38px;
  color: white;
}

.fa-file-alt { 
  color: rgb(250, 173, 57);
}

.fa-cut {
  color: rgb(243, 225, 61);
}

.fa-hand-rock {
  color: rgb(49, 49, 49);
}

#fas-target1 {
  margin: 20px;
  font-size: 98px;
  cursor: pointer;
}

#fas-target2{
  margin: 20px;
  font-size: 98px;
  cursor: pointer;
}

span {
  margin: 5px;
}

#userstar {
  background: yellow;
}

.Player2 p{
  text-align: center;
}

.Rock, .Paper, .Scissor {
  transform: scale(1.1);
  
}

#fas-target1:hover {
  transform: scale(.9);
  transition: all 0.2s;
}

#fas-target1:active {
  transform: scale(.9);
  background-color:  #032744;
}

#newGame:enabled {
  background-color: #499ce0;
}

#newGame:disabled {
    color: -internal-light-dark(rgba(16, 16, 16, 0.3), white);
    background-color: -internal-light-dark(rgba(239, 239, 239, 0.3), rgba(19, 1, 1, 0.3));
    border-color: -internal-light-dark(rgba(118, 118, 118, 0.3), rgba(195, 195, 195, 0.3));
}
</style>

 <!--
table tr:nth-child(even) {
  background-color: rgb(150, 150, 150);
}
 -->