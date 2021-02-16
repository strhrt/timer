<template>
  <div id="app">
    <div class="timer">
      <div class="timer__time">{{ humanMinutes }}.{{ humanSeconds }}.{{ humanMilliseconds }}</div>
      <div class="timer__buttons">
        <i v-if="isStarted" class="material-icons" @click="pauseTimer">pause</i>
        <i v-else class="material-icons" @click="startTimer">play_arrow</i>
        <i class="material-icons" @click="addMinute">add</i>
        <i class="material-icons" @click="removeMinute">remove</i>
        <i class="material-icons" @click="stopTimer">stop</i>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      timer: null,
      isStarted: false,
      minutes: 1,
      seconds: 10,
      milliseconds: 9,
      duration: 70009
    }
  },
  computed: {
    humanMinutes() {
      return this.minutes < 10 ? `0${this.minutes}` : this.minutes
    },
    humanSeconds() {
      return this.seconds < 10 ? `0${this.seconds}` : this.seconds
    },
    humanMilliseconds() {
      if (this.milliseconds < 10) return `00${this.milliseconds}`
      if (this.milliseconds < 100) return `0${this.milliseconds}`
      return this.milliseconds
      // return this.milliseconds < 10 ? `0${this.milliseconds}` : this.milliseconds
    }
    // duration() {
    //   console.log(this.minutes, this.seconds, this.milliseconds)
    //   return this.minutes * 60000 + this.seconds * 1000 + this.milliseconds
    // }
  },
  beforeDestroy() {
    this.pauseTimer()
  },
  methods: {
    pauseTimer() {
      console.log('pause')
      clearInterval(this.timer)
      this.isStarted = false
    },
    startTimer() {
      console.log('start')
      // const interval = 0.01

      this.isStarted = true
      console.log(this.duration)

      this.timer = setInterval(() => {
        if (!this.duration) this.stopTimer()

        this.duration -= 11
        this.minutes = Math.floor(this.duration / 60000)
        this.seconds = Math.floor((this.duration / 1000) % 60)
        this.milliseconds = Math.round(this.duration % 1000)
      }, 11)
    },
    // setTime() {
    //   console.log('test')
    // },
    addMinute() {
      console.log('plus')
    },
    removeMinute() {
      console.log('minus')
    },
    stopTimer() {
      console.log('test')
      clearInterval(this.timer)
      this.isStarted = false
    }
  }
}
</script>

<style lang="scss">
* {
  margin: 0;
  padding: 0;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  font-weight: bold;
  color: #202830;
  display: flex;
  flex-flow: row nowrap;
  align-items: center;
  justify-content: center;
  height: 100vh;
  width: 100%;
}
.timer {
  height: 300px;
  background: yellow;
  width: 360px;
  display: flex;
  flex-flow: column nowrap;
  align-items: center;
  justify-content: center;
  &__time {
    font-size: 4rem;
  }
  &__buttons {
    display: flex;
    flex-flow: row nowrap;
    justify-content: center;
    .material-icons {
      cursor: pointer;
      margin: 0 0.6rem;
      font-size: 2.6rem;
    }
  }
}
</style>
