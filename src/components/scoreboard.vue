<template>
  <div id="score">
      
      <div class="board" >
          <span class="user">{{ name1 }}</span>
          <span @change="justifyMarks" class="score"> {{ score1 }} : {{ score2 }} </span>
          <span class="comp">{{ name2 }}</span>
      </div>    

      <div class="noti">
          <p v-if='score1 == 3'> Winner {{ name1 }} </p>
          <p v-if='score2 == 3 '> Winner {{ name2 }} </p>
      </div>
  </div> 
</template>

<script>
export default {
    name: 'Scoreboard',
    props: {
        name1: {
            type: String,
            default: 'User'
        },
        name2: {
            type: String,
            default: 'Comp'
        },
        score1: {
            type: Number,
        },
        score2: {
            type: Number,
        }
    },
    data () {
        return {
            fscore1: this.score1,
            sscore2: this.score2,
        }
    },

    methods: {
        justifyMarks() {
           this.fscore1 = this.score1
           this.sscore2 = this.score2
           
           if(this.fscore1 == 3 || this.sscore2 == 3) this.fscore1 = 0; this.sscore2 = 0  
        }
    }
}
</script>

<style>

* {
    text-align: center;
}

body, html {
    margin: 20px;
    width: auto;
    
}

.board {
    color: white;
    font-size: 48px;
    padding: 60px;
}

.board .score {
    padding: 70px;
    border-left: 1px solid white;
    border-right: 1px solid white;
}

.board span {
    background-color: #2167a0;
}

.board .user {
    position: relative;
    left: 2.3rem;
    
}

.board .comp {   
    position: relative;
    right: 2.3rem;
}

.noti {
    font-size: 48px;
}


</style>