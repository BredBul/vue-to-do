<template>
  <main class="container">
    <add-resource></add-resource>
    <stored-resources id="convert-to-pdf"></stored-resources>
    <div class="container">
      <base-button @click="savePDF">Save in pdf</base-button>
    </div>
  </main>
</template>
<script>
import StoredResources from './StoredResources.vue';
import AddResource from './AddResource.vue';
import html2canvas from 'html2canvas';
import jsPDF from 'jspdf';
import BaseButton from '../UI/BaseButton.vue';

export default {
  components: {
    StoredResources,
    AddResource,
    BaseButton,
  },
  data() {
    return {
      storedResources: [
        {
          id: 1,
          title: 'First',
          description: 'First description',
        },
        {
          id: 2,
          title: 'Second',
          description: 'Second description',
        },
      ],
    };
  },
  provide() {
    return {
      resources: this.storedResources,
      addNewResource: this.addNewResource,
      deleteResource: this.removeResource,
      saveEditing: this.saveEditing,
    };
  },
  methods: {
    savePDF() {
      window.html2canvas = html2canvas;
      let doc = new jsPDF('l', 'pt');
      doc.html(document.querySelector('#convert-to-pdf'), {
        callback: function (pdf) {
          pdf.save('vue-list.pdf');
        },
      });
    },
    addNewResource(newTitle, newDesc) {
      const newResource = {
        id: Date.now(),
        title: newTitle,
        description: newDesc,
      };
      this.storedResources.unshift(newResource);
    },
    removeResource(resId) {
      const resIndex = this.storedResources.findIndex(
        (res) => res.id === resId
      );
      this.storedResources.splice(resIndex, 1);
    },
    saveEditing(newTitle, newDesc, resId) {
      const resIndex = this.storedResources.findIndex(
        (res) => res.id === resId
      );
      this.storedResources[resIndex].title = newTitle;
      this.storedResources[resIndex].description = newDesc;
    },
  },
};
</script>
<style>
.container {
  max-width: 40rem;
  margin: 0 auto;
  padding: 0px 10px;
}
</style>
