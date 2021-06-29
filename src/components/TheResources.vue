<template>
  <base-card>
    <base-button
      :mode="storedResourcesButton"
      @click="switchTab('stored-resources')"
      >Stored Resources</base-button
    >
    <base-button :mode="addResourceButton" @click="switchTab('add-resource')">
      Add Resource</base-button
    >
  </base-card>
  <keep-alive><component :is="selectedTab"></component></keep-alive>
</template>

<script>
import { ref, computed, provide } from "vue";
import StoredResources from "./StoredResources.vue";
import AddResource from "./AddResource.vue";
import BaseButton from "./BaseButton";
import BaseCard from "./BaseCard";

export default {
  components: {
    StoredResources,
    AddResource,
    BaseButton,
    BaseCard
  },
  setup() {
    // Data
    const selectedTab = ref("stored-resources");
    const storedResources = ref([
      {
        id: "official-guide",
        title: "Official Guide",
        description: "The official Vue.js documentation",
        link: "https://vuejs.org"
      },
      {
        id: "google",
        title: "Google",
        description: "Your Favorite Search Engine",
        link: "https://google.com"
      }
    ]);

    // Methods
    const switchTab = tab => {
      selectedTab.value = tab;
    };

    const saveResource = (title, description, link) => {
      const newResource = {
        id: new Date().toUTCString(),
        title: title,
        description: description,
        link: link
      };

      storedResources.value.unshift(newResource);
      selectedTab.value = "stored-resources";
    };

    const removeResource = resourceId => {
      const indexValue = storedResources.value.findIndex(
        resource => resource.id === resourceId
      );
      storedResources.value.splice(indexValue, 1);
    };

    // Computed Properties
    const storedResourcesButton = computed(() => {
      return selectedTab.value === "stored-resources" ? null : "flat";
    });

    const addResourceButton = computed(() => {
      return selectedTab.value === "add-resource" ? null : "flat";
    });

    // Provide
    provide("resources", storedResources);
    provide("saveResource", saveResource);
    provide("removeResource", removeResource);

    return {
      selectedTab,
      storedResources,
      storedResourcesButton,
      addResourceButton,
      removeResource,
      saveResource,
      switchTab
    };
  }
};
</script>

<style></style>
