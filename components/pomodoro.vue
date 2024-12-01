<template>
  <div id="container">
    <h1>25 + 5 Clock</h1>
    <div id="controls">

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

    <div id="clock">{{ displayMinutes }}:<h1 v-show="zero">0</h1>{{ displaySeconds }}</div>

    <div class="adjust-length">
      <h3>controls</h3>
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
      audio: new Audio('https://codeskulptor-demos.commondatastorage.googleapis.com/descent/gotitem.mp3')
    }
  },

  methods: {
    setCountdown(x) {
      this.displayMinutes = x,
        this.displaySeconds = '00',
        clearInterval(this.interval);
      this.interval = null;

    },
    updateCountdown() {


      if (this.displayMinutes === 0 && this.displaySeconds === 0) {
        this.displaySeconds = '00',
          this.displayMinutes = '00'
        clearInterval(this.interval);
        this.audio.play()
      }

      if (this.displaySeconds === '00') {
        this.displayMinutes -= 1;
        this.displaySeconds = 59;
      } else {
        this.displaySeconds -= 1;
        this.zero = false
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
    },
  }
}
</script>

<style>
* {
  margin: 0;
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
  font-family: sans-serif;
  font-size: 34px;
}

.adjust-length {
  width: 210px;
  height: 140px;
  margin: auto;
  text-align: center;
  font-size: 20px;
}

#controls {
  display: flex;
  flex-direction: row;
}

button {
  width: 100px;
  height: 50px;
  border-radius: 5px;
  font-size: larger;
  background-color: black;
  color: lime;
  box-shadow: rgba(9, 255, 0, 0.612) 0px 2px 4px, rgba(0, 0, 0, 0.3) 0px 7px 13px -3px, rgba(0, 0, 0, 0.2) 0px -3px 0px inset;
}

#clock {
  min-width: 500px;
  max-width: 30vw;
  min-height: 20vh;
  max-height: 40vh;

  margin: auto;
  margin-top: 30px;
  font-size: 200px;
  text-align: center;
  color: limegreen;
}

h3 {
  color: lime;
}
</style>