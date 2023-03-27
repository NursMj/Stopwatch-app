<template>
  <div class="app">
    <stopwatch v-for='i in stopwatcshAmount' />
    <button class="add-btn" @click="addStopwatch">
      <img src="./assets/img/add.svg" alt="">
    </button>

  </div>

</template>

<script>
  import Stopwatch from './components/Stopwatch.vue'

  export default {
    components: {
      Stopwatch
    },
    data() {
      return {
        stopwatcshAmount: 3,
      }
    },
    methods: {
      addStopwatch() {
        this.stopwatcshAmount++
      }
    }
  }
</script>

<style >
  .app {
    display: grid;
    grid-template-columns: 1fr 1fr 1fr;
    row-gap: 45px;
    column-gap: 50px;
    margin: 0 auto;
    padding: 72px 0;
    width: 775px;
    justify-content: space-between;
    user-select: none; 
  }

  .add-btn {
    display: flex;
    justify-content: center;
    align-items: center;
    width: 225px;
    height: 120px;
    background: #696969;
    color: #9E9E9E;
    border: none;
    cursor: pointer;
  }

  @media (max-width: 820px) {
    .app {
      width: 500px;
      grid-template-columns: 1fr 1fr;
    } 
  }

  @media (max-width: 550px) {
    .app {
      width: 225px;
      grid-template-columns: 1fr;
    } 
  }
</style>
