<template>
  <div class="photo-grid">
    <Photo
      v-for="photo in photos"
      :key="photo.id"
      :photo="photo"
    />
    <p v-if="!photos.length" class="no-results">Nenhuma foto encontrada.</p>
  </div>
</template>

<script setup>
import { defineProps } from "vue";
import Photo from "./Photo.vue";

defineProps({
  photos: {
    type: Array,
    required: true,
  },
});
</script>

<style scoped>
.photo-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
  gap: 1rem;
  padding: 1rem;
}
.no-results {
  grid-column: 1 / -1;
  text-align: center;
  color: #999;
}
</style>
