<template>
  <div class="home">
    <Jokes />
  </div>
</template>

<script lang="ts">
import Jokes from "@/components/Jokes.vue";
import { defineComponent } from "vue";

export default defineComponent({
  components: { Jokes },
  name: "Home",
});
</script>
