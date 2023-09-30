<template>
  <div class="container">
    <div class="advice-card">
      <p>ADVICE {{ '#' + id }}</p>
      <h1>{{ advice }}</h1>
      <img src="pattern-divider-mobile.svg" alt="pattern divider" />
    </div>
    <div @click="getAdvice" class="dice-container">
      <img src="icon-dice.svg" alt="dice icon" />
    </div>
  </div>
</template>

<script>
export default {
  name: 'App',

  data() {
    return {
      advice: undefined,
      id: undefined,
    };
  },

  methods: {
    getAdvice() {
      this.axios
        .get('https://api.adviceslip.com/advice')
        .then(
          (response) => (
            (this.id = response.data.slip.id),
            (this.advice = response.data.slip.advice)
          )
        );
    },
  },

  created() {
    this.getAdvice();
  },
};

//	https://api.adviceslip.com/advice
</script>

<style scoped>
@import './style.css';

.container {
  width: 100vw;
  height: 100vh;
  display: grid;
  place-items: center;
}
.advice-card {
  max-width: 37.5rem;
  max-height: 20rem;
  width: 90%;
  height: 50%;
  background-color: var(--DarkGrayishBlue);
  border-radius: 1rem;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: space-evenly;
  text-align: center;
  position: relative;
}

.dice-container {
  background-color: var(--NeonGreen);
  position: absolute;
  bottom: 9rem;
  display: flex;
  align-items: center;
  padding: 1rem;
  border-radius: 50%;
  cursor: pointer;
}

.rotate-dice {
  transform: rotate(360deg);
  transition: ease 0.5s;
}

@media screen and (min-width: 600px) {
  .dice-container {
    bottom: 10rem;
  }
}
</style>
