<script setup lang="ts">
import { RouterView } from "vue-router";
</script>

<template>
  <RouterView />
</template>

<style>
html,
body,
#app {
  margin: 0;
  padding: 0;
  height: 100%;
  font-family: "Spoqa Han Sans Neo";
}
h1,
h2,
h3,
p {
  margin: 0;
  padding: 0;
}
button {
  border: none;
  background-color: transparent;
  padding: 0;
  cursor: pointer;
  outline: none;
}
ul {
  list-style: none;
  padding: 0;
  margin: 0;
}
ol {
  margin: 0;
}
input {
  background: none;
  border: none;
  color: inherit;
}
a {
  text-decoration: none;
  color: inherit;
}
address {
  font-style: normal;
}
* {
  box-sizing: border-box;
}
iframe {
  position: absolute;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  border: 0;
}
</style>
