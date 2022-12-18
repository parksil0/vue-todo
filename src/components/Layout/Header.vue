<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  name: "HeaderComponent",
  setup() {},
});
</script>

<template>
  <header>
    <h1 class="title">My Tasks</h1>
  </header>
</template>

<style scoped>
.title {
  font-weight: 700;
  font-size: 48px;
  line-height: 78px;
  letter-spacing: 0.25em;
  text-align: center;
}
</style>
