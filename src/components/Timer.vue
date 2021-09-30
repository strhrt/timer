<template>
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
      <i v-else class="material-icons" @click="startTimerHandler">play_arrow</i>
      <i class="material-icons" @click="addMinute">add</i>
      <i class="material-icons" @click="removeMinute">remove</i>
      <i class="material-icons" @click="stopTimer">stop</i>
    </div>
  </div>
</template>

<script>
const DEFAULT_TIME_IN_MILLISECONDS = 600000
const MILLISECONDS_IN_ONE_MINUTE = 60000

export default {
  data() {
    return {
      timer: null,
      isStarted: false,
      duration: DEFAULT_TIME_IN_MILLISECONDS
    }
  },
  computed: {
    humanMinutes() {
      const minutes = Math.floor(this.duration / MILLISECONDS_IN_ONE_MINUTE)
      return minutes < 10 ? `0${minutes}` : minutes
    },
    humanSeconds() {
      const seconds = Math.floor((this.duration / 1000) % 60)
      return seconds < 10 ? `0${seconds}` : seconds
    },
    humanMilliseconds() {
      const milliseconds = Math.round(this.duration % 1000)
      if (milliseconds === 0) return '00'
      return milliseconds < 100 ? milliseconds : Math.floor(milliseconds / 10)
    }
  },
  beforeDestroy() {
    this.pauseTimer()
  },
  methods: {
    startTimerHandler() {
      this.startTimer()
    },
    startTimer() {
      this.isStarted = true

      if (!this.duration) {
        this.clearTimer()
        return
      }
      this.duration -= 10

      const timerId = setTimeout(() => {
        if (this.timer === timerId) {
          this.startTimer()
        } else {
          this.timer = null
        }
      }, 10)

      this.timer = timerId
    },
    pauseTimer() {
      this.clearTimer()
    },
    clearTimer() {
      clearInterval(this.timer)
      this.timer = null
      this.isStarted = false
    },
    addMinute() {
      this.duration += MILLISECONDS_IN_ONE_MINUTE
    },
    removeMinute() {
      if (this.duration > MILLISECONDS_IN_ONE_MINUTE) this.duration -= MILLISECONDS_IN_ONE_MINUTE
      else this.duration = 0
    },
    stopTimer() {
      this.clearTimer()
      this.resetValuesToDefault()
    },
    resetValuesToDefault() {
      this.duration = DEFAULT_TIME_IN_MILLISECONDS
    }
  }
}
</script>

<style lang="scss" scoped>
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
    display: flex;
    p {
      min-width: 74px;
    }
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
