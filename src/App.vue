<template>
  <body>
    <form class="donate-form" @submit.prevent="addDonate">
      <h1 id="total-amount">${{ total }}</h1>
      <label class="donate-form__input-label">
        Введите сумму в $
        <input
          class="donate-form__donate-input"
          name="amount"
          type="number"
          max="100"
          min="1"
          required=""
        />
      </label>
      <button class="donate-form__submit-button" type="submit">
        Задонатить
      </button>
    </form>
    <div class="donates-container">
      <h2 class="donates-container__title">Список донатов</h2>
      <!-- <div class="donates-container__donates"> -->
      <DonatesView :donates="donates" />
      <!-- </div> -->
    </div>
  </body>
</template>

<script>
const options = {
  weekday: "short",
  year: "numeric",
  month: "short",
  day: "numeric",
  hour: "numeric",
  minute: "numeric",
  second: "numeric",
  hour12: false,
};

import DonatesView from "./components/DonatesView";

export default {
  name: "App",
  components: {
    DonatesView,
  },
  data() {
    return {
      donates: [],
    };
  },
  methods: {
    addDonate() {
      event.preventDefault();
      const amount = Number(event.target.amount.value);
      const date = new Date().toLocaleDateString("ru-RU", options);
      const newDonate = {
        id: this.donates.length + 1,
        amount,
        date,
      };
      this.donates.push(newDonate);
    },
  },
  created() {
    this.donates = [
      {
        id: 1,
        amount: 1,
        date: new Date().toLocaleDateString("ru-RU", options),
      },
      {
        id: 2,
        amount: 3,
        date: new Date().toLocaleDateString("ru-RU", options),
      },
      {
        id: 3,
        amount: 20,
        date: new Date().toLocaleDateString("ru-RU", options),
      },
      {
        id: 4,
        amount: 4,
        date: new Date().toLocaleDateString("ru-RU", options),
      },
    ];
  },
  computed: {
    total() {
      return this.donates.reduce((acc, cur) => acc + cur.amount, 0);
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

:root {
  --main-background: #4666b1;
  --primary-color: #4666b1;
  --default-text-color: #ffffff;
  --donate-item-text-color: #000000;
  --default-border-color: #ffffff;
}

body {
  padding: 0;
  margin: 0;
  min-height: 100vh;
  max-height: 100vh;
  height: 100vh;

  display: flex;
  justify-content: space-evenly;

  flex-wrap: wrap;
  padding: 20px;
  overflow: hidden;

  color: var(--default-text-color);
  background: var(--main-background);
  box-sizing: border-box;
}

.donates-container {
  display: flex;
  flex-direction: column;

  list-style: none;
  border-left: 10px solid var(--primary-color);
  padding: 0;
  height: 75%;
  width: 40%;
  overflow: hidden;
}

.donates-container .donate-item {
  padding: 10px;
}

.donates-container .donate-item:nth-child(odd) {
  background: #e1f1ff;
}

.donates-container .donate-item:nth-child(even) {
  background: white;
}

.donate-item {
  color: var(--donate-item-text-color);
}

.donate-form {
  display: flex;
  flex-direction: column;
  justify-content: center;

  height: 75%;
}

#total-amount {
  font-size: 3rem;
  line-height: 3rem;
}

.donate-form__donate-input {
  font-size: 2rem;
  line-height: 2rem;

  background: var(--primary-color);
  color: var(--default-border-color);
  border: 2px solid var(--default-border-color);
  border-radius: 5px;

  margin-top: 5px;
}

.donate-form__input-label {
  font-size: 2rem;
  line-height: 2rem;

  display: flex;
  flex-direction: column;
}

.donates-container__donates {
  overflow: auto;
  height: 100%;
  flex-grow: 1;
}

.donate-form__submit-button {
  font-size: 2rem;
  line-height: 2.5rem;
  cursor: pointer;

  border: 2px solid var(--default-border-color);
  border-radius: 5px;
  color: var(--default-text-color);
  background: none;
  transition: 0.3s ease;
  box-shadow: none;

  margin-top: 30px;
}

.donate-form__submit-button:hover {
  color: var(--primary-color);
  background: var(--default-text-color);
}

.donate-form__submit-button:focus {
  box-shadow: 0 0 0 2px var(--default-border-color);
}

@media (max-width: 720px) {
  body {
    flex-direction: column;
    align-items: center;
    justify-content: initial;
    flex-wrap: initial;
    padding: 10px;
  }

  .donates-container,
  .donate-form {
    height: initial;
    width: 80%;
  }

  .donates-container__title {
    font-size: 2rem;
    line-height: 2.5rem;
  }

  #total-amount {
    font-size: 3.5rem;
    line-height: 4rem;
    text-align: center;
  }

  .donate-form__donate-input,
  .donate-form__submit-button {
    height: 50px;
  }
}
</style>
