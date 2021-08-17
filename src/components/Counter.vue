<template>
  <div v-if="counter > 0" class="counter">
    <p>A modal box is going to appear in {{ counter }} seconds</p>
  </div>
</template>

<script>
import { defineComponent, ref, onMounted } from "vue";

export default defineComponent({
  name: "CounterComponent",
  setup() {
    let counter = ref(25);

    // FUNCTIONS

    function counterFrom25To0() {
      // Decrease counter by 1 every second
      setInterval(() => {
        counter.value--;
      }, 1000);
    }

    // MOUNTED
    onMounted(() => {
      counterFrom25To0();
    });

    return {
      counter: counter,
      counterFrom25To0: counterFrom25To0,
    };
  },
});
</script>

<style></style>
