<script setup>
</script>

<template>
  <header>
    <h2>calc-vue</h2>
  </header>
  <div class="container">
    <div class="display">
      <div class="display__last-operation">
        <span class="display__last-operation__text">
          20 / 5
        </span>
      </div>
      <input type="text" class="display__text">
    </div>
  </div>
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
  width: 80%;
  margin: 0 auto;
  height: 100%;
  background-color: black;
  border-radius: 5px;
}

.display {
  display: flex;
  align-items: center;
  justify-content: center;
  height: 100px;
  width: 100%;
  background-color: #232323;
  margin: 30px;
  border-left: solid 6px #E83D2A;
  border-radius: 5px;
  position: relative;

  .display__last-operation {
    position: absolute;
    top: 10px;
    right: 15px;
    color: white;
  }

  .display__text {
    width: 400px;
    height: 50px;
    background-color: transparent;
    /* border: solid 1px white; */
    border: none;
    position: absolute;
    bottom: 10px;
    right: 13px;
    font-size: 60px;
    color: white;
    text-align: right;
    font-weight: 500;
  }

  .display__text:focus {
    outline: none;
  }
}
</style>
