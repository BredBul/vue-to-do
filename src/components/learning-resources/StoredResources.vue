<template>
  <ul>
    <learning-resource
      v-for="res in resources"
      :key="res.id"
      :id="res.id"
      :title="res.title"
      :description="res.description"
    ></learning-resource>
  </ul>
</template>

<script>
import LearningResource from './LearningResource';
export default {
  inject: ['resources'],
  components: {
    LearningResource,
  },
};
</script>

<style scoped>
ul {
  list-style: none;
  padding: 0;
  margin: 0 auto;
  max-width: 40rem;
}
</style>
