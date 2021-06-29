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
import { inject } from "vue";
import SingleResource from "./SingleResource";

export default {
  components: {
    SingleResource
  },
  setup() {
    const resources = inject("resources");
    return { resources };
  }
};
</script>

<style scoped>
ul {
  list-style: none;
  padding: 0;
}
</style>
