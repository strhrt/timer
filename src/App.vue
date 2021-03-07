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
      // default values
      minutes: 0,
      seconds: 2,
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
      if (this.milliseconds < 10) return `0${this.milliseconds}` // correct display when 0
      if (this.milliseconds >= 100) return Math.floor(this.milliseconds / 10)
      return this.milliseconds
    },
    duration() {
      return this.minutes * 60000 + this.seconds * 1000 + this.milliseconds
    }
  },
  watch: {},
  beforeDestroy() {
    this.pauseTimer()
  },
  methods: {
    startTimer() {
      if (!this.duration) return
      this.isStarted = true

      this.timer = setInterval(() => {
        const time = this.duration - 10

        this.minutes = Math.floor(time / 60000)
        this.seconds = Math.floor((time / 1000) % 60)
        this.milliseconds = Math.round(time % 1000)
        // stop when duration is 0
        if (!time) this.clearTimer()
      }, 10)
    },
    pauseTimer() {
      this.clearTimer()
    },
    clearTimer() {
      clearInterval(this.timer)
      this.isStarted = false
    },
    addMinute() {
      this.minutes += 1
    },
    removeMinute() {
      if (this.minutes > 0) this.minutes -= 1
    },
    stopTimer() {
      this.clearTimer()
      // reset to default values
      this.minutes = 10
      this.seconds = 0
      this.milliseconds = 0
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
