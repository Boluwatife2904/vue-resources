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
  data() {
    return {
      selectedTab: "stored-resources",
      storedResources: [
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
      ]
    };
  },
  provide() {
    return {
      resources: this.storedResources,
      saveResource: this.saveResource,
      removeResource: this.removeResource
    };
  },
  computed: {
    storedResourcesButton() {
      return this.selectedTab === "stored-resources" ? null : "flat";
    },
    addResourceButton() {
      return this.selectedTab === "add-resource" ? null : "flat";
    }
  },
  methods: {
    switchTab(tab) {
      this.selectedTab = tab;
    },
    saveResource(title, description, link) {
      const newResource = {
        id: new Date().toUTCString(),
        title: title,
        description: description,
        link: link
      };
      this.storedResources.unshift(newResource);
      this.selectedTab = "stored-resources";
    },
    removeResource(resourceId) {
      const indexValue = this.storedResources.findIndex(
        resource => resource.id === resourceId
      );
      this.storedResources.splice(indexValue, 1);
    }
  }
};
</script>

<style></style>
