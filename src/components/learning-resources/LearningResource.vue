<template>
  <li @add-resource="addNewResource">
    <base-card class="container">
      <div>
        <h3 v-if="!editing">{{ title }}</h3>
        <p v-if="!editing">{{ description }}</p>
        <div class="input-edit" v-if="editing">
          <input v-model="newTitle" />
          <input v-model="newDesc" />
          <p v-if="isValid">Both fields must be field</p>
        </div>
      </div>

      <div>
        <base-button @click="deleteResource(id)">Delete</base-button>
        <base-button v-if="!editing" @click="editResource">Edit</base-button>
        <base-button v-if="editing" @click="disableEditing">Cancel</base-button>
        <base-button
          :disabled="isValid"
          v-if="editing"
          @click="
            saveEditing(newTitle, newDesc, id);
            disableEditing();
          "
        >
          Save
        </base-button>
      </div>
    </base-card>
  </li>
</template>

<script>
export default {
  props: ['id', 'title', 'description'],
  inject: ['deleteResource', 'saveEditing'],
  data() {
    return {
      editing: false,
      newTitle: null,
      newDesc: null,
    };
  },
  computed: {
    isValid() {
      if (this.newTitle === '' || this.newDesc === '') return true;
      else return false;
    },
  },
  methods: {
    editResource() {
      this.newTitle = this.title;
      this.newDesc = this.description;
      this.editing = true;
    },
    disableEditing() {
      this.newTitle = null;
      this.newDesc = null;
      this.editing = false;
    },
  },
};
</script>

<style scoped>
li {
  margin: auto;
  max-width: 40rem;
}

.container {
  display: flex;
  justify-content: space-between;
  align-items: center;
}
.input-edit {
  display: flex;
  flex-direction: column;
}

h3 {
  font-size: 1.25rem;
  margin: 0.5rem 0;
}

p {
  margin: 0.5rem 0;
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
