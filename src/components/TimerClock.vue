<template>
  <div class="timer-container">
    <div class="timer">
      <div class="timer-box">
        <p class="timer-text">{{ timerType }}: {{ formatTime(timerCount) }}</p>
      </div>
      <button @click="start" class="modern-button">Start</button>
      <button @click="stop" class="modern-button">Stop</button>
      <button @click="restart" class="modern-button">Restart</button>
      <button @click="endSession" class="modern-button">End Session</button>
    </div>
  </div>
</template>

<script>
import Swal from 'sweetalert2'
export default {
  data () {
    return {
      timerEnabled: false,
      timerCount: 50, // 50 seconds (minutes would be 50 * 60)
      timerType: 'Session',
      timerIntervalId: null
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
      this.timerCount = 50
      this.timerType = 'Session'
      this.startTimer()
    },
    endSession () {
      this.timerEnabled = false
      this.timerCount = 10
      this.timerType = 'Break'
      this.startTimer()
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
      clearInterval(this.timerIntervalId)
    },
    handleTimerEnd () {
      if (this.timerType === 'Session') {
        this.timerCount = 10
        this.timerType = 'Break'
        this.startTimer()
        Swal.fire({
          title: 'Session is over',
          confirmButtonColor: '#5b5b5b',
          cancelButtonColor: '#888d82',
          howCancelButton: true,
          confirmButtonText: 'Start the break'
        }).then((result) => {
          if (result.isConfirmed) {
            this.timerEnabled = true
            this.startTimer()
          }
        })
      } else {
        this.timerCount = 50
        this.timerType = 'Session'
        Swal.fire({
          title: 'The Break Ended',
          confirmButtonColor: '#5b5b5b',
          cancelButtonColor: '#888d82',
          showCancelButton: true,
          confirmButtonText: 'Start a new session'
        }).then((result) => {
          if (result.isConfirmed) {
            this.restart()
            this.timerEnabled = true
            this.startTimer()
          }
        })
      }
    },
    formatTime (seconds) {
      const minutes = Math.floor(seconds / 60)
      const remainingSeconds = seconds % 60
      return `${minutes}:${remainingSeconds < 10 ? '0' : ''}${remainingSeconds}`
    }
  }
}

</script>

<style scoped>
.timer-container {
  display: flex;
  justify-content: flex-start;
  align-items: center;
  height: 0vh;
  padding-left: 20px;
  padding-top: 40px;
}
.timer-box {
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 2px;
  border-radius: 10px;
  background-color: #ffffff;
  margin-bottom: 2px;
}
.timer {
  text-align: center;
  padding: 20px;
  border-radius: 20px;
  background-color: #f2f2f2;
}
.timer-text {
  font-family: 'San Francisco', sans-serif; /* Use the San Francisco font for modernity */
  font-size: 35px; /* Adjust the font size as needed */
  font-weight: bold;
  margin-bottom: -3px;
}
.modern-button {
  background-color: #888d82;
  color: white;
  border: none;
  border-radius: 20px;
  padding: 10px 20px;
  cursor: pointer;
  margin: 5px;
  transition: background-color 0.3s ease, transform 0.3s ease;
}

.modern-button:hover {
  background-color: #5b5b5b;
  transform: scale(1.1);
}
</style>
