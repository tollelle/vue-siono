<template>
  <div class="box" :style="image">
    <img :src="src">
    <h1>{{ answer }}</h1>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      answer: "",
      src: "",
      image: {
        backgroundImage: "",
        backgroundSize: "contain",
        backgroundPosition: "center",
        backgroundRepeat: "no-repeat"
      }
    };
  },

  mounted() {
    axios
      .get("https://yesno.wtf/api")
      .then(res => {
        this.answer = res.data.answer;
        this.image.backgroundImage = `url(${res.data.image})`;
        this.src = res.data.image;
      })
      .catch(err => {
        this.answer = "¡ERROR!";
        console.error(err);
      });
  }
  /*
  mounted() {
    fetch("https://yesno.wtf/api")
      .then(response => response.json())
      .then(data => {
        this.answer = data.answer;
        this.image.backgroundImage = `url(${data.image})`;
      })
      .catch(err => {
        this.answer = "¡ERROR! :(";
        console.error(err);
      });
  }
  */
};
</script>

<style>
</style>