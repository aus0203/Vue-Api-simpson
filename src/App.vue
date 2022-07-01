<template>
  <div class="main">
    <div class="top-section">
      <img :src="image" class="simpson-pic" />
      <div class="quote-section">
        <p>{{ character }}</p>
        <span v-if="quote?.length > 0">:</span>
        <p>{{ quote }}</p>
      </div>
    </div>

    <button class="main-button" @click="getSimpson">Simpson wisdom</button>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      showQuote: false,
      image: "",
      quote: null,
      character: "",
    };
  },

  methods: {
    async getSimpson() {
      try {
        const resp = await axios.get(
          "https://thesimpsonsquoteapi.glitch.me/quotes"
        );
        console.log(resp);
        this.image = resp.data[0].image;
        this.quote = resp.data[0].quote;
        this.character = resp.data[0].character;
      } catch (error) {
        console.log(error);
      }

      this.showQuote = !this.showQuote;
    },
  },
};
</script>

<style>
* {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}

body {
  background: #111111;
  color: #ffffff;
  font-family: 'Roboto', sans-serif;

}

p{
  font-size: 14px;
}

.main {
  display: flex;
  width: 100vw;
  height: 100vh;
  justify-content: center;
  flex-direction: column;
  align-items: center;
  gap: 20px;
}



.simpson-pic{
  width: 200px;
}

.top-section{
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  gap: 12px;
}

.quote-section {
  display: flex;
  flex-direction: row;
  gap: 8px;
}

.main-button {
  padding: 8px 12px;
  background: transparent;
  color:#ffffff;
  border: 1px solid #ffffff;
  border-radius: 8px;
}

.main-button:hover{
  background: #343434;
  transition: 200ms ease-in-out;
}
</style>
