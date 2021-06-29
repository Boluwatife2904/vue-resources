<template>
  <ul>
    <single-resource
      v-for="resource in resources"
      :key="resource.id"
      :title="resource.title"
      :id="resource.id"
      :description="resource.description"
      :link="resource.link"
    ></single-resource>
  </ul>
</template>

<script>
import SingleResource from "./SingleResource";

export default {
  components: {
    SingleResource
  },
  inject: ["resources"]
};
</script>

<style scoped>
ul {
  list-style: none;
  padding: 0;
  margin: 0 auto;
  max-width: 40rem;
  width: 100%;
}
</style>
