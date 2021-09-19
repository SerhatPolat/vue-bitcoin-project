<template>
  <div id="app">
    <div class="header">
      <img src="./assets/bitcoin.png" />
      <h1>Bitcoin</h1>
    </div>
    <div :class="theme === 'light' ? 'lightTheme' : 'darkTheme'" class="main">
      <div class="themeSwitchDiv">
        <p>Dark Mode:</p>
        <input @click="switchTheme" type="checkbox" />
      </div>
      <div class="box">
        <h1>Bitcoin Price</h1>
        <div v-for="currency in info" v-bind:key="currency.id" class="currency">
          {{ currency.description }}:
          <span class="lighten">
            <span v-html="currency.symbol"></span>{{ currency.rate }}
          </span>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "App",

  data() {
    return {
      info: null,
      theme: "light",
    };
  },

  mounted() {
    axios
      .get("https://api.coindesk.com/v1/bpi/currentprice.json")
      .then((response) => (this.info = response.data.bpi));
  },

  methods: {
    switchTheme() {
      this.theme = this.theme === "dark" ? "light" : "dark";
    },
  },
};
</script>

<style>
* {
  font-family: Franklin Gothic Medium;
}

.header {
  display: flex;
  background-color: black;
  border-top-right-radius: 10px;
  border-top-left-radius: 10px;
  justify-content: center;
}

.header h1 {
  color: white;
}

.header img {
  height: 50px;
  margin-top: 12px;
  margin-right: 10px;
  margin-left: -20px;
}

.main {
  height: 100%;
}

.box {
  width: 85%;
  margin: auto;
  padding: 20px;
  border-radius: 10px;
  padding-top: 50px;
  text-align: center;
  padding-bottom: 200px;
}

.box h1 {
  margin-top: 0;
  margin-bottom: 50px;
  text-decoration: underline;
}

.lightTheme {
  background-color: white;
  color: black;
}

.darkTheme {
  background-color: black;
  color: white;
}

.themeSwitchDiv {
  width: 113px;
  margin: auto;
  display: flex;
}

.themeSwitchDiv input {
  accent-color: white;
  margin-left: 10px;
  height: 20px;
  width: 20px;
  margin-top: 15px;
}
</style>
