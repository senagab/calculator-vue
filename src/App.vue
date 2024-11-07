<script setup>
</script>

<template>
  <header>
    <h2>calc-vue</h2>
  </header>
  <!-- CONTAINER -->
  <div class="container">

    <!-- DISPLAY -->
    <div class="display">
      <div class="display__last-operation">
        <span class="display__last-operation__text">
          20 / 5 =
        </span>
      </div>
      <input type="text" class="display__text">
    </div>

    <!-- TECLADO -->
    <div class="keyboard">
      <div class="keyboard__left">
        <div class="keys">7</div>
        <div class="keys">8</div>
        <div class="keys">9</div>
        <div class="keys">4</div>
        <div class="keys">5</div>
        <div class="keys">6</div>
        <div class="keys">1</div>
        <div class="keys">2</div>
        <div class="keys">3</div>
        <div class="keys">0</div>
        <div class="keys" style="color: gray;">,</div>
        <div class="keys" style="color: gray;">√</div>
      </div>
      <div class="keyboard__center">
        <div class="keys">/</div>
        <div class="keys">x</div>
        <div class="keys">-</div>
        <div class="keys">+</div>
      </div>
      <div class="keyboard__right">
        <div class="keys">del</div>
        <div class="keys">clear</div>
        <div class="keys" style="height: 21vh;">enter</div>
        <!-- <div class="keys">enter</div> -->
      </div>
    </div>
  </div>
    <!-- FIM DO CONTAINER -->
</template>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Inter:ital,opsz,wght@0,14..32,100..900;1,14..32,100..900&display=swap');


* {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
  font-family: 'Inter', sans-serif;
}

header {
  color: #bdbdbd;
}

.container {
  display: flex;
  flex-direction: column;
  width: 40%;
  margin: 0 auto;
  height: 100%;
  background-color: black;
  border-radius: 5px;
}

.display {
  display: flex;
  align-items: center;
  justify-content: center;
  height: 20vh;
  width: auto;
  background-color: #232323;
  margin: 30px;
  border-left: solid 6px #E83D2A;
  border-radius: 5px;
  position: relative;

  .display__last-operation {
    position: absolute;
    top: 20px;
    right: 15px;
    color: rgb(150, 150, 150);
  }

  .display__text {
    width: 400px;
    height: 60px;
    background-color: transparent;
    /* border: solid 1px white; */
    border: none;
    position: absolute;
    bottom: 25px;
    right: 13px;
    font-size: 5em;
    color: white;
    text-align: right;
    font-weight: 500;
    caret-color: transparent;
  }

  .display__text:focus {
    outline: none;
  }
}

.keyboard {
  margin: -15px 30px 30px;
  display: flex;
  justify-content: space-around;

  .keyboard__left {
    display: grid;
    grid-template-columns: 1fr 1fr 1fr;
    gap: 1rem;

    .keys {
      width: 10vh;
      height: 10vh;
      border: 1px solid #232323;
      display: flex;
      justify-content: center;
      align-items: center;
      background-color: black;
      font-size: 30px;
      color: white;
    }
    
    .keys:hover {
      background-color: #232323;
      cursor: pointer;
    }
  }

  .keyboard__center {
    display: grid;
    grid-template-columns: 1fr;
    gap: 1rem;

    .keys {
      width: 10vh;
      height: 10vh;
      display: flex;
      justify-content: center;
      align-items: center;
      background-color: black;
      font-size: 30px;
      color: rgb(138, 138, 138);
      border: 1px solid #232323;
    }
    
    .keys:hover {
      background-color: #232323;
      cursor: pointer;
    }
  }

  .keyboard__right {
    display: grid;
    grid-template-columns: 50px;
    grid-template-rows: 1fr 1fr 2fr;
    gap: 1rem;
    margin: 0 15px;

    .keys {
      width: 7vh;
      height: 10vh;
      display: flex;
      justify-content: center;
      align-items: center;
      background-color: black;
      padding: 30px;
      font-size: 30px;
      color: rgb(138, 138, 138);
      border: 1px solid #232323;
    }

    .keys:hover {
      background-color: #232323;
      cursor: pointer;
    }
  }
}



</style>
