<template>
  <div id="container">
    <div id="set-time">
      <div class="adjust-length">
        <h3>Session Length</h3>
        <button @click=setCountdown(25)>25m</button>
        <button @click=setCountdown(45)>45m</button>
      </div>
      <div class="adjust-length">
        <h3>Break Length</h3>
        <button @click=setCountdown(15)>15m</button>
        <button @click=setCountdown(5)>5m</button>
      </div>
    </div>

    <div id="clock">
      <span v-show="minutesZero">0{{ displayMinutes }}</span><span v-show="!minutesZero">{{ displayMinutes
        }}</span>:<span v-show="secondsZero">0{{ displaySeconds }}</span><span v-show="!secondsZero">{{ displaySeconds
        }}</span>
    </div>

    <div id="controls">
      <button @click="startCountdown">start</button>
      <button @click="pauseCountdown">pause</button>
      <button @click="resetCountdown">reset</button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      displayMinutes: 25,
      displaySeconds: '00',
      interval: null,
      audio: new Audio('https://codeskulptor-demos.commondatastorage.googleapis.com/descent/gotitem.mp3'),
      secondsZero: false,
      minutesZero: false
    }
  },
  methods: {
    setCountdown(x) {
      this.displayMinutes = x,
        this.displaySeconds = '00',
        clearInterval(this.interval); this.interval = null;
      if (x < 10) {
        this.minutesZero = true
      } else {
        this.minutesZero = false
      }
    },
    updateCountdown() {
      if (this.displayMinutes === 0 && this.displaySeconds === 0) {
        this.displaySeconds = '00',
          this.displayMinutes = '00'
        clearInterval(this.interval);
        this.audio.play()
        this.secondsZero = false;
        this.minutesZero = false;
        return
      } else if (this.displaySeconds === '00' || this.displaySeconds === 0) {
        this.displayMinutes--;
        this.displaySeconds = 59;
        this.secondsZero = false;
        if (this.displayMinutes <= 9 && this.displayMinutes != 0) {
          this.minutesZero = true;
        }
      } else if (this.displaySeconds <= 10 && this.displaySeconds != 0) {
        this.displaySeconds--
        this.secondsZero = true;
      } else {
        this.secondsZero = false;
        this.displaySeconds--
      }
    },
    startCountdown() {
      if (!this.interval) {
        this.interval = setInterval(this.updateCountdown, 1000);
      }
    },
    pauseCountdown() {
      clearInterval(this.interval);
      this.interval = null;
    },
    resetCountdown() {
      clearInterval(this.interval);
      this.interval = null;
      this.displayMinutes = 25;
      this.displaySeconds = '00';
      this.secondsZero = false
      this.minutesZero = false
    },
  }
}
</script>

<style>
* {
  margin: auto;
  font-family: sans-serif;
  color: rgba(0, 255, 0, 0.752);
}

#container {
  border: 2px solid black;
  width: 100vw;
  height: 100vh;
  margin: auto;
  background-color: black;
}

h1 {
  min-width: 150px;
  max-width: 25%;
  text-align: center;
  margin-left: auto;
  margin-right: auto;
  font-size: 34px;
}

.adjust-length {
  width: 240px;
  height: 100px;
  text-align: center;
  font-size: 20px;
}

.adjust-length button {
  width: 45%;
  height: 60%;
}

#controls {
  display: flex;
  flex-direction: row;
  justify-content: space-around;
  align-items: center;
  height: 100px;
  width: 500px;
}

#controls button {
  width: 31%;
  height: 75%;
  font-size: 26px;
}

#set-time {
  display: flex;
  flex-direction: row;
  width: 500px;
  height: 100px;
  margin-top: 10%;
}

button {
  width: 100px;
  height: 50px;
  border-radius: 5px;
  font-size: larger;
  background-color: black;
  box-shadow: rgba(9, 255, 0, 0.612) 0px 2px 4px,
    rgba(0, 0, 0, 0.3) 0px 7px 13px -3px,
    rgba(0, 0, 0, 0.2) 0px -3px 0px inset;
}

#clock {
  width: 500px;
  height: 200px;
  margin: auto;
  font-size: 200px;
  line-height: 100%;
}

@media (max-width: 600px) {
  #clock {
    font-size: 100px;
    width: 250px;
    height: 100px;
    margin: auto;
    line-height: 100%;
  }
  #set-time {
  display: flex;
  flex-direction: row;
  width: 250px;
  height: 50px;
  margin-top: 10%;
}
#controls {
  display: flex;
  flex-direction: row;
  justify-content: space-around;
  align-items: center;
  height: 50px;
  width: 250px;
}
.adjust-length button {
  width: 59px;
  height: 30%;
}
.adjust-length {
  font-size: 14px;
}
}
</style>