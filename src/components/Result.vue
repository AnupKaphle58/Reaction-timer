<template>
  <div class="result" v-if="!showError">
    <p>Reaction Time: {{ score }} ms</p>
    <p class="rank">{{ rank }}</p>
  </div>
</template>

<script>
export default {
  props: ['score'],
  data(){
    return{
      rank:null
    }
  },
  mounted(){
    if (this.score <250){
      this.rank = 'Ninja Finger'
    } else if (this.score < 400){
      this.rank = 'Rapid Reflex'
    } else {
      this.rank = 'Snail pace ...'
    }
  },
}
</script>

<style>
.rank{
  font-size: 1.4em;
  color: 0faf87;
  font-weight: bold;
}
</style>
