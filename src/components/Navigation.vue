<template>
  <div id="nav">
    <router-link to="/">Home</router-link>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  name: "Navigation",
});
</script>

<style lang="scss">
#nav {
  padding: 30px;

  a {
    font-weight: bold;
    color: #2c3e50;
    font-size: 1.4rem;

    &.router-link-exact-active {
      color: black;
    }
  }
}
</style>
