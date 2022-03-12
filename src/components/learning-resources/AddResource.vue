<template>
  <div>
    <base-card>
      <form @submit.prevent="submitData">
        <div class="form-control">
          <label for="title">Title</label>
          <input ref="titleInput" id="title" name="title" type="text" />
        </div>
        <div class="form-control">
          <label for="description">Description</label>
          <textarea
            ref="descriptionInput"
            name="description"
            id="description"
            rows="3"
          ></textarea>
        </div>
        <div>
          <base-button type="submit">Add The Note</base-button>
        </div>
        <div class="form-error">
          <p v-if="inputIsInvalid">
            Both the title and the description must be filled in.
          </p>
        </div>
      </form>
    </base-card>
  </div>
</template>
<script>
import BaseButton from '../UI/BaseButton.vue';
export default {
  components: { BaseButton },
  inject: ['addNewResource'],
  data() {
    return {
      inputIsInvalid: false,
    };
  },
  methods: {
    submitData() {
      const titleValue = this.$refs.titleInput.value;
      const descriptionValue = this.$refs.descriptionInput.value;
      if (titleValue.trim() === '' || descriptionValue.trim() === '') {
        this.inputIsInvalid = true;
        return false;
      } else {
        this.inputIsInvalid = false;
        this.addNewResource(titleValue, descriptionValue);
      }
    },
  },
};
</script>
<style scoped>
label {
  font-weight: bold;
  display: block;
  margin-bottom: 0.5rem;
}

input,
textarea {
  display: block;
  width: 100%;
  font: inherit;
  padding: 0.15rem;
  border: 1px solid #ccc;
}

input:focus,
textarea:focus {
  outline: none;
  border-color: #3a0061;
  background-color: #f7ebff;
}

.form-control {
  margin: 1rem 0;
}
.form-error {
  color: red;
}
</style>
