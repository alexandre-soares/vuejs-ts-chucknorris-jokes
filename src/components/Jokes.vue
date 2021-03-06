<template>
  <Loading v-if="isLoading" />
  <div class="jokes">
    <h2>{{ joke.text }}</h2>
    <p>Rate this joke</p>
    <div class="buttons">
      <button @click="rateJoke('bad')">😩</button>
      <button @click="rateJoke('medium')">🤨</button>
      <button @click="rateJoke('good')">😂</button>
    </div>
    <button class="btn" @click="getRandomJoke">Get Another Joke</button>
    <div class="notifications">
      <transition-group name="slide-fade" mode="out-in">
        <p
          v-for="(notification, index) in notifications"
          :key="index"
          :class="notification.rating"
          @click="removeNotification(index)"
        >
          {{ notification.text }}
        </p>
      </transition-group>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref, onMounted } from "vue";
import axios from "axios";

import Loading from "../components/Loading.vue";

export default defineComponent({
  name: "Jokes",
  components: {
    Loading,
  },
  setup() {
    // Declare variables
    let isLoading = ref(false);
    let joke = { id: "1", text: "String" };
    const notifications = ref([
      {
        id: "1",
        text: "This is a notification",
        rating: "good",
      },
    ]);

    // Get a joke
    async function getRandomJoke(): Promise<void> {
      // Start the loading screen
      isLoading.value = true;

      // Api Call
      try {
        const response = await axios.get(
          "https://api.chucknorris.io/jokes/random"
        );

        // Assign and display the joke
        joke.id = response.data.id;
        joke.text = response.data.value;

        // Stop the loading screen
        isLoading.value = false;
      } catch (error) {
        console.error(error);
      }
    }

    // Rate a joke
    function rateJoke(value: string) {
      // Push the notification object on the notifications array

      const newNotification = {
        id: joke.id,
        text: "",
        rating: value,
      };

      if (value === "bad") {
        newNotification.text = `You didn't like the joke: ${joke.text}!`;
      }
      if (value === "medium") {
        newNotification.text = `The joke "${joke.text}" didn't impress you!`;
      }
      if (value === "good") {
        newNotification.text = `You liked the joke: ${joke.text}`;
      }

      notifications.value.push(newNotification);

      // Api Call for another joke
      getRandomJoke();
    }

    // Auto Remove Notifications
    function autoRemoveNotification() {
      // Remove the oldest notification only if there is at least one
      if (notifications.value.length > 0) {
        notifications.value.shift();
      }
    }

    // Remove the notifications

    function removeNotification(index: number) {
      notifications.value.splice(index, 1);
    }

    onMounted(() => {
      getRandomJoke();

      setInterval(() => {
        autoRemoveNotification();
      }, 10000);
    });

    return {
      isLoading: isLoading,
      joke: joke,
      notifications: notifications,
      getRandomJoke: getRandomJoke,
      rateJoke: rateJoke,
      autoRemoveNotification: autoRemoveNotification,
      removeNotification: removeNotification,
    };
  },
});
</script>

<style lang="scss" scoped>
.jokes {
  display: flex;
  flex-direction: column;
  align-items: center;
  width: 80%;
  margin: 0 auto 4rem;
  background-color: white;
  padding: 3rem 4rem;
  margin-top: 5rem;
  border-radius: 1.5rem;
  & h2 {
    font-size: 2rem;
    line-height: 1.6;
    text-align: center;
    text-transform: capitalize;
  }
}
.buttons {
  display: flex;
  align-items: center;
  justify-content: space-between;
  & button {
    font-size: 6rem;
    padding: 1.5rem;
    background-color: transparent;
    border: none;
    cursor: pointer;
    transition: all 0.5s ease-in-out;
    margin: 0.5rem;
    &:nth-child(2) {
      margin-top: 5rem;
    }
    @media only screen and (max-width: $bp-medium) {
      font-size: 4rem;
    }
    &:hover {
      background-color: rgba(141, 141, 141, 0.493);
    }
  }
}
.notifications {
  position: absolute;
  bottom: 1rem;
  right: 1rem;
  width: 50%;
  p {
    padding: 2rem 3rem;
    text-align: right;
    margin: 2rem;
    border-radius: 1.5rem;
    font-size: 1.4rem;
    cursor: pointer;
  }
  & .bad {
    background-color: #f8d7da;
    color: #842029;
  }
  & .medium {
    background-color: #fff3cd;
    color: #735b14;
  }
  & .good {
    color: #0f5132;
    background-color: #d1e7dd;
  }
}
.btn {
  height: 5rem;
}
// ANIMATIONS
/* Enter and leave animations can use different */
/* durations and timing functions.              */
.slide-fade-enter-active {
  transition: all 0.3s ease;
}
.slide-fade-leave-active {
  transition: all 0.5s cubic-bezier(1, 0.5, 0.8, 1);
}
.slide-fade-enter, .slide-fade-leave-to
/* .slide-fade-leave-active below version 2.1.8 */ {
  transform: translateX(4rem);
  opacity: 0;
}
</style>
