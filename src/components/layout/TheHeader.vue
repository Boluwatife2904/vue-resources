<template>
  <header>
    <h3>{{ title }}</h3>
  </header>
</template>

<script>
export default {
  name: "Header",
  props: ["title"]
};
</script>

<style scoped>
header {
  background: #ce5c00;
  padding: 40px 10px;
  width: 100%;
  margin-bottom: 50px;
}

header h3 {
  color: #fff;
  text-align: center;
}
</style>
