<template>
  <the-header title="Vue.js Resources"></the-header>
  <the-resources></the-resources>
</template>

<script>
import TheHeader from "./components/layout/TheHeader";
import TheResources from "./components/TheResources";

export default {
  name: "App",
  components: {
    TheHeader,
    TheResources
  }
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Karla:wght@300;400;500;600;700&display=swap");

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

html {
  scroll-behavior: smooth;
}

body {
  font-family: "Karla", sans-serif;
}
</style>
