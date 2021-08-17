<template>
  <Navigation />
  <router-view />
</template>

<script lang="ts">
import { defineComponent } from "vue";
import Navigation from "./components/Navigation.vue";

export default defineComponent({
  name: "App",
  components: {
    Navigation,
  },
});
</script>

<style lang="scss">


#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
  font-family: "Poppins", sans-serif;
}

html {
  font-size: 62.5%; // 1rem = 10px
  overflow-x: hidden;
  @media only screen and (max-width: $bp-large) {
    font-size: 60%;
  }
}

body {
  background-color: #fbab7e;
  background-image: linear-gradient(62deg, #fbab7e 0%, #f7ce68 100%);
  width: 100vw;
  height: 100vh;
}

.btn {
  padding: 1rem 2rem;
  border-radius: 0.5rem;
  border: none;
  cursor: pointer;
  transition: all 0.3s ease-in-out;
  margin: 2rem;

  &:hover {
    color: white;
    background-color: darkgray;
  }

  &:active {
    transform: translateY(0.5rem);
  }
}

p {
  font-size: 1.6rem;
  margin: 1rem;
  line-height: 1.6;
}
</style>
