<template>
  <div>
    <p>{{ timerType }}: {{ formatTime(timerCount) }}</p>
    <button @click="start">Start</button>
    <button @click="stop">Stop</button>
    <button @click="restart">Restart</button>
    <button @click="endSession">End Session</button>
  </div>
</template>

<script>
export default {
  data () {
    return {
      timerEnabled: false,
      timerCount: 50, // 50 seconds (minutes would be 50 * 60)
      timerType: 'Session',
      timerIntervalId: null // To keep track of the interval ID
    }
  },
  watch: {
    timerEnabled (value) {
      if (value) {
        this.startTimer()
      }
    },
    timerCount (value) {
      if (value === 0) {
        this.timerEnabled = false
        this.handleTimerEnd()
      }
    }
  },
  methods: {
    start () {
      this.timerEnabled = true
    },
    stop () {
      this.timerEnabled = false
      this.clearTimerInterval()
    },
    restart () {
      this.timerCount = 50 // 50 seconds (minutes would be 50 * 60)
      this.timerType = 'Session'
      this.startTimer()
    },
    endSession () {
      this.timerEnabled = false
      this.timerCount = 10 // 10 seconds (minutes would be 10 * 60)
      this.timerType = 'Break'
      this.startTimer() // Start the break timer immediately
    },
    startTimer () {
      this.clearTimerInterval()
      this.timerIntervalId = setInterval(() => {
        if (this.timerCount > 0 && this.timerEnabled) {
          this.timerCount--
        }
      }, 1000)
    },
    clearTimerInterval () {
      clearInterval(this.timerIntervalId)// Bugfix clear the time to make start stop work if pressed after eachother
    },
    handleTimerEnd () {
      if (this.timerType === 'Session') {
        // Switch to break timer (10 minutes)
        this.timerCount = 10 // 10 seconds (minutes would be 10 * 60)
        this.timerType = 'Break'
        this.startTimer()
      } else {
        this.timerCount = 50 // 50 seconds (minutes would be 50 * 60)
        this.timerType = 'Session'
      }
      // Optionally, you can add a notification or some indication that a new phase has started.
      // For example: alert(`Time for ${this.timerType}!`);
    },
    formatTime (seconds) {
      const minutes = Math.floor(seconds / 60)
      const remainingSeconds = seconds % 60
      return `${minutes}:${remainingSeconds < 10 ? '0' : ''}${remainingSeconds}`
    }
  }
}
</script>
