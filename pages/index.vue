<template>
<client-only>
  <body>
    <div class="advice">
      <p class="advice__id">Advice #{{ adviceId }}</p>
      <p class="advice__text">{{ adviceText }}</p>
      <div class="divider__desktop"><img src="../assets/pattern-divider-desktop.svg" alt=""></div>
      <div class="divider__mobile"><img src="../assets/pattern-divider-mobile.svg" alt=""></div>
      <button class="button" @click="generateNewAdvice"><img src="../assets/icon-dice.svg" alt="Button to generate new advice"></button>
    </div>
  </body>
</client-only>
</template>

<script>

import axios from "axios";

export default {
  name: 'IndexPage',
  data() {
    return {
      adviceId: null,
      adviceText: null,
    }
  },

  async mounted() {
    const res = await axios.get('https://api.adviceslip.com/advice');
    const data = res.data.slip;
    this.adviceId = data.id;
    this.adviceText = data.advice;

  },

  methods: {
    async generateNewAdvice() {
      const res = await axios.get('https://api.adviceslip.com/advice');
      const data = res.data.slip  
      this.adviceId = data.id;
      this.adviceText = data.advice;
    }
  },
}
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Manrope:wght@200;300;400;500;600;700;800&display=swap");

* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
    background-color: #202632;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    height: 100vh;
    font-family: 'Manrope', sans-serif;
}

.advice {
    background-color: hsl(217, 19%, 24%);
    padding: 60px 50px;
    width: 500px;
    border-radius: 10px;
    color: #cee3e9;
    text-align: center;
    position: relative;
    display: flex;
    flex-direction: column;
    align-items: center;
}

.advice__id {
    color: hsl(150, 100%, 66%);
    text-transform: uppercase;
    font-weight: 700;
    letter-spacing: 5px;
}
.advice__text {
    font-weight: 800;
    font-size: 28px;
    margin: 35px 0;
}

.divider__mobile {
  display: none;
}

.button {
    border-radius: 50%;
    width: 65px;
    height: 65px;
    padding: 20px;
    background-color: hsl(150, 100%, 66%);
    border: none;
    position: absolute;
    bottom: 0;
    transform: translateY(50%);
    cursor: pointer;
    transition: 0.5s;
}

.button:hover {
    box-shadow: 0 0 35px hsl(150, 100%, 66%);
}


    @media (max-width:600px) {
      .advice {
        width: 340px;
      }

      .divider__desktop {
        display: none;
      }

      .divider__mobile {
        display: inline;
      }
    }
</style>
