<template>
  <div class="stopwatch" :class="{active: isActive}">
    <div class="display">
      <span>{{ time }}</span>
    </div>
    <div class="btns">
      <div v-if="!isActive" class="btn" @click="start">
        <svg class="btn__svg" width="17" height="20" viewBox="0 0 17 20" xmlns="http://www.w3.org/2000/svg">
          <path d="M0 20V0L17 10L0 20Z"/>
        </svg> 
      </div>
      <div v-else class="btn" @click="stop">
        <svg class="btn__svg" width="10" height="20" viewBox="0 0 10 20" xmlns="http://www.w3.org/2000/svg">
          <rect x="7" width="3" height="20" />
          <rect width="3" height="20"/>
        </svg>
      </div>
      <div class="btn" @click="reset">
        <svg class="btn__svg" width="20" height="20" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg">
          <rect width="20" height="20"/>
        </svg>
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    name: "stopwatch",
    data() {
      return {
        time: '0',
        total: 0,
        timer: null,
        isActive: false,
      }
    },
    methods: {
      start() {
        this.isActive = !this.isActive

        this.timer = setInterval(() => {
          this.total += 1

          const hours = Math.floor(this.total / 3600 % 24);
          const minutes = Math.floor(this.total / 60 % 60);
          const seconds = Math.floor(this.total % 60);

          if (this.total >= 3600) {
            this.time = `${hours}:${minutes}:${seconds}`
          } else if (this.total >= 60) {
            this.time = `${minutes}:${seconds}`
          } else {
            this.time = seconds
          }
        }, 1000)
      },
      stop() {
        this.isActive = !this.isActive
        clearInterval(this.timer)
      },
      reset() {
        this.isActive = false
        clearInterval(this.timer)
        this.total = 0
        this.time = '0'
      }
    }
  }
</script>

<style scoped>
  .stopwatch {
    width: 225px;
    background: #696969;
    color: #9E9E9E;
    fill: #9E9E9E;
  }
  .stopwatch.active {
    color: #fff;
    fill: #fff;
  }
  .display {
    position: relative;
    display: flex;
    justify-content: center;
    padding: 20px 0;
    font-size: 22px;
    line-height: 20px;
  }
  .display::after {
    position: absolute;
    bottom: 0;
    content: "";
    display: block;
    width: 100%;
    height: 1px;
    background-color: #9E9E9E;
  }
  .active .display::after {
    background-color: #fff;
  }
  .btns {
    display: flex;
    justify-content: space-between;
    padding: 20px 70px;
  }
  .btn {
    cursor: pointer;
  }
  .btn__svg {
    display: block;
  }
</style>
