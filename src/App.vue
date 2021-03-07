<template>
  <div id="app">
    <div class="timer">
      <div class="timer__time">
        <p id="min">{{ humanMinutes }}</p>
        .
        <p id="sec">{{ humanSeconds }}</p>
        .
        <p id="milli">{{ humanMilliseconds }}</p>
      </div>
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
      minutes: 123,
      seconds: 5,
      milliseconds: 0
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
      if (this.milliseconds < 10) return `0${this.milliseconds}`
      if (this.milliseconds >= 100) return Math.floor(this.milliseconds / 10)
      return this.milliseconds
    },
    duration() {
      console.log(this.minutes, this.seconds, this.milliseconds)
      return this.minutes * 60000 + this.seconds * 1000 + this.milliseconds
    }
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
      let time = this.duration
      if (!time) return
      this.isStarted = true

      this.timer = setInterval(() => {
        time -= 10
        this.minutes = Math.floor(time / 60000)
        this.seconds = Math.floor((time / 1000) % 60)
        this.milliseconds = Math.round(time % 1000)
        if (time < 10) {
          this.stopTimer()
        }
      }, 10)
    },
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
  background-color: #383a3b;

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
    display: flex; //temporary
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
