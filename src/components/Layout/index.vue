<script lang="ts">
import HeaderComponent from "./Header.vue";

export default {
  name: "LayoutComponent",
  components: {
    HeaderComponent,
  },
};
</script>

<template>
  <main class="main">
    <HeaderComponent />
    <slot />
  </main>
</template>

<style scoped>
.main {
  width: 1280px;
  padding: 32px 232px;
  margin: 0 auto;

  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 24px;
}
</style>
