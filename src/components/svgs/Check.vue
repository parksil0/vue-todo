<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  name: "CheckIcon",
  props: {
    isFinished: Boolean,
  },
  computed: {
    setColor() {
      return this.isFinished ? "green" : "black";
    },
  },
});
</script>

<template>
  <svg
    width="30"
    height="30"
    viewBox="0 0 30 30"
    fill="none"
    xmlns="http://www.w3.org/2000/svg"
  >
    <path
      d="M27 13.3572V14.5072C26.9985 17.2027 26.1256 19.8255 24.5117 21.9844C22.8977 24.1434 20.6291 25.7228 18.0442 26.487C15.4593 27.2513 12.6966 27.1595 10.1681 26.2254C7.6396 25.2912 5.48082 23.5648 4.0137 21.3035C2.54658 19.0422 1.84974 16.3672 2.0271 13.6775C2.20445 10.9879 3.24651 8.42756 4.99785 6.3785C6.74919 4.32943 9.11598 2.90138 11.7452 2.30734C14.3745 1.71329 17.1253 1.98508 19.5875 3.08216"
      :style="{ stroke: setColor, transition: 'stroke 0.1s ease-in-out' }"
      stroke-width="2"
      stroke-linecap="round"
      stroke-linejoin="round"
    />
    <path
      d="M20 11L12.3077 19L10 16.6024"
      :style="{ stroke: setColor, transition: 'stroke 0.1s ease-in-out' }"
      stroke-width="2"
      stroke-linecap="round"
      stroke-linejoin="round"
    />
  </svg>
</template>
