<template>
  <li>
    <base-card>
      <header>
        <h3>{{ title }}</h3>
        <base-button mode="flat" @click="removeResource(id)">
          Delete
        </base-button>
      </header>
      <p>{{ description }}</p>
      <a :href="link" target="_blank" rel="noopener noreferrer">Visit Site</a>
    </base-card>
  </li>
</template>

<script>
import { inject } from "vue";
import BaseCard from "./BaseCard";
import BaseButton from "./BaseButton";

export default {
  name: "SingleResource",
  components: {
    BaseCard,
    BaseButton
  },
  props: {
    id: {
      required: true
    },
    title: {
      type: String,
      required: true
    },
    description: {
      type: String,
      required: true
    },
    link: {
      type: String,
      required: true
    }
  },
  setup() {
    const removeResource = inject("removeResource");
    return { removeResource };
  }
};
</script>

<style scoped>
header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 20px;
}

h3 {
  font-size: 1.25rem;
  margin: 0;
}

p {
  margin: 0 0 15px;
}

a {
  text-decoration: none;
  color: #ce5c00;
}

a:hover,
a:active {
  color: #c89300;
}
</style>
