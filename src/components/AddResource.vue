<template>
  <base-dialog v-if="invalidInput" @close="closeDialog" title="Error!!!">
    <template #default>
      <p>Unfortunately, one or more input field are incorrect</p>
      <p>
        Ensure that you have filled all inputs correctly and have entered at
        least some characters
      </p>
    </template>
    <template #actions>
      <base-button @click="closeDialog">Okay</base-button>
    </template>
  </base-dialog>
  <base-card>
    <form @submit.prevent="submitResource">
      <div class="form-control">
        <label for="title">Title</label>
        <input type="text" name="title" id="title" v-model="title" />
      </div>
      <div class="form-control">
        <label for="description">Description</label>
        <textarea
          name="description"
          id="description"
          cols="30"
          rows="3"
          v-model="description"
        ></textarea>
      </div>
      <div class="form-control">
        <label for="link">Link</label>
        <input type="url" name="link" id="link" v-model="link" />
      </div>
      <div>
        <base-button>Add Resource</base-button>
      </div>
    </form>
  </base-card>
</template>

<script>
import { ref, inject } from "vue";
import BaseButton from "./BaseButton.vue";
import BaseCard from "./BaseCard.vue";
import BaseDialog from "./BaseDialog.vue";

export default {
  name: "AddResource",
  components: {
    BaseCard,
    BaseButton,
    BaseDialog
  },
  setup() {
    const title = ref("");
    const description = ref("");
    const link = ref("");
    const invalidInput = ref(false);
    const saveResource = inject("saveResource");

    const submitResource = () => {
      if (
        title.value.trim() === "" ||
        description.value.trim() === "" ||
        link.value.trim() === ""
      ) {
        invalidInput.value = true;
      } else {
        saveResource(title.value, description.value, link.value);
      }
      title.value = "";
      description.value = "";
      link.value = "";
    };

    const closeDialog = () => {
      invalidInput.value = false;
    };

    return {
      title,
      description,
      link,
      invalidInput,
      submitResource,
      closeDialog
    };
  }
};
</script>

<style>
label {
  font-weight: bold;
  display: inline-block;
  margin-bottom: 12px;
}

input,
textarea {
  display: block;
  width: 100%;
  font: inherit;
  padding: 12px 30px 12px 10px;
  border: 1px solid #ccc;
  border-radius: 4px;
}

input:focus,
textarea:focus {
  outline: none;
  border-color: #3a0061;
  background-color: #f7ebff;
}

.form-control {
  margin-bottom: 25px;
}

p {
  margin-bottom: 10px;
  line-height: 30px;
}
</style>
