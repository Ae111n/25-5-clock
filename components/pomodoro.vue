<template>
  <div id="container">
    <h1>25 + 5 Clock</h1>
    <div id="controls">
      <div class="adjust-length">
        <h3>Break Length</h3>
        <button class="arrow">+</button>
        <span>25:00</span>
        <button class="arrow">-</button>
      </div>
      <div class="adjust-length">
        <h3>Session Length</h3>
        <button class="arrow">+</button>
        <span>25:00</span>
        <button class="arrow">-</button>
      </div>
    </div>

    <div id="clock"></div>
  </div>
</template>

<script>
export default {
  data() {
    return {
    }
  },
  methods: {

  }




}
</script>

<style>
#container {
  border: 2px solid black;
  width: 98vw;
  height: 98vh;
  margin: auto;

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

  width: 250px;
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

  width: 40px;
  height: 40px;
  border-radius: 20px;
}
#clock {
  min-width: 500px;
  max-width :70vw;
  min-height: 40vh;
  max-height: 100vh;
  border: 2px solid purple;
  margin: auto;
  margin-top: 30px;
}
</style>