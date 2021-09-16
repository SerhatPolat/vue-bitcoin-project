<template>
  <div id="app">
    <div class="header">
      <img src="./assets/bitcoin.png" />
      <h1>Bitcoin</h1>
    </div>
    <div class="main">
      <div class="box">
        <h1>Bitcoin Price Index</h1>
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
    };
  },
  mounted() {
    axios
      .get("https://api.coindesk.com/v1/bpi/currentprice.json")
      .then((response) => (this.info = response.data.bpi));
  },
};
</script>

<style>
html {
  height: 100%;
  background-color: #000063;
}

* {
  font-family: Franklin Gothic Medium;
}

.header {
  display: flex;
  border-bottom: 2px solid white;
  justify-content: center;
}

.header h1 {
  color: white;
}

.header img {
  height: 50px;
  margin-top: 12px;
  margin-right: 10px;
}

.main {
  background-color: #000063;
  height: 100%;
}

.box {
  width: 85%;
  margin: auto;
  color: black;
  background-color: white;
  padding: 20px;
  border-radius: 10px;
  margin-top: 50px;
  text-align: center;
}

.box h1 {
  margin-top: 0;
  margin-bottom: 50px;
}
</style>
