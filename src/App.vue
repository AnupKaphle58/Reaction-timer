<template>
  <h1>Reaction Timer</h1>
  <div v-if="!isPlaying">
      Click Play to start <br/>
  </div>
  <button @click="start" :disabled="isPlaying">Play</button>
  <div class="guideline" v-if="!isPlaying && !showResult && !showError" >
    <h2>Green block will appear here</h2>
    Press green block as soon as it appears<br/>
    Don't press too early
  </div>
  <div>
    <div class="invisible-block" @click="clickError" v-if="isPlaying && !showResult" v-show="showInvisibleBlock" ></div>
    <Block v-if="isPlaying" :delay="delay" @end='endGame' @showB='clickError'/>
  </div>

  <Result v-if="showResult" :score='score' />
  <EarlyPress v-if="showError" class="early-press" />
</template>

<script>
import Block from './components/Block.vue'
import Result from './components/Result.vue'
import EarlyPress from './components/EarlyPress.vue'
export default {
  name: 'App',
  components: { Block, Result, EarlyPress},
  data() {
    return {
      isPlaying: false,
      delay: null,
      score: null,
      showResult: false,
      showInvisibleBlock: false,
      showError: false
    }
  },
  methods: {
    start() {
      this.delay = 2000 + Math.random() * 5000
      setTimeout(() => {
        this.showInvisibleBlock =false
      }, this.delay)
      this.isPlaying = true
      this.showResult = false
      this.showError = false
      this.showInvisibleBlock =true
    },
    endGame(reactionTime){
      this.score = reactionTime
      this.isPlaying = false
      this.showResult =true
    },
    clickError(){
      this.isPlaying = false
      this.showResult = false
      this.showError = true
    },
  },
}
</script>

<style>
  #app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #444;
    margin-top: 60px;
  }
  button {
    background: #0faf87;
    color: white;
    border: none;
    padding: 8px 16px;
    border-radius: 4px;
    font-size: 16px;
    letter-spacing: 1px;
    cursor: pointer;
    margin: 10px;
  }
  button[disabled] {
    opacity: 0.2;
    cursor: not-allowed;
  }
  .guideline {
     width: 400px;
     border: dotted;
     border-width: 4px;
     border-radius: 20px;
     background:  #ddd;
     color: #0faf87;
     text-align: center;
     padding: 100px 0;
     margin: 40px auto;
   }
   .invisible-block {
     width: 600px;
     border-radius: 20px;
     background: black;
     color: white;
     text-align: center;
     padding: 100px 0;
     margin: 40px auto;
   }
.early-press{
  background: red;
}
</style>
