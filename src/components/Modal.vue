<template>
  <div class="modal" v-if="modalOpen">
    <div class="modal__box">
      <h1>Hope you like it!</h1>
      <p>
        Don't hesitate to send me an email at <br />
        alexandre.desousasoares@gmail.com
      </p>
      <iframe
        src="https://giphy.com/embed/BIuuwHRNKs15C"
        width="480"
        height="359"
        frameBorder="0"
        class="giphy-embed"
        allowFullScreen
      ></iframe>
      <p>
        <a href="https://giphy.com/gifs/chuck-norris-thumbs-up-BIuuwHRNKs15C"
          >via GIPHY</a
        >
      </p>
      <span class="modal__close" @click="closeModal">
        <img :src="require(`@/assets/close.svg`)" alt="close" />
      </span>
    </div>
  </div>
</template>

<script lang="ts">
export default {
  data() {
    return {
      modalOpen: false,
    };
  },
  mounted() {
    setTimeout(() => {
      this.openModal();
    }, 25000);
  },
  methods: {
    openModal(): void {
      this.modalOpen = true;
    },
    closeModal(): void {
      this.modalOpen = !this.modalOpen;
    },
  },
};
</script>

<style lang="scss" scoped>
.modal {
  position: absolute;
  top: 0;
  left: 0;
  height: 100vh;
  width: 100vw;
  z-index: 9999;
  background-color: rgba(0, 0, 0, 0.479);
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
  &__box {
    position: relative;
    background-color: white;
    height: 50%;
    width: 80%;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
  }
  &__close {
    position: absolute;
    font-size: 3rem;
    top: 1rem;
    right: 2rem;
    cursor: pointer;
    & img {
      height: 3rem;
    }
  }
}
</style>
