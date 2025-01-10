<template>
  <div id="app">
    <Header />
    <SearchBar v-model="searchQuery" />
    <PhotoGrid :photos="filteredPhotos" />
    <Footer />
  </div>
</template>

<script setup>
import { ref, computed, onMounted } from "vue";
import Header from "./components/Header.vue";
import Footer from "./components/Footer.vue";
import SearchBar from "./components/SearchBar.vue";
import PhotoGrid from "./components/PhotoGrid.vue";

const searchQuery = ref("");
const photos = ref([]);

const fetchPhotos = async () => {
  try {
    const response = await fetch("https://jsonplaceholder.typicode.com/photos?_limit=10");
    if (!response.ok) {
      throw new Error(`Erro HTTP! Status: ${response.status}`);
    }
    photos.value = await response.json();
  } catch (error) {
    console.error("Erro ao carregar fotos:", error);
  }
};

onMounted(fetchPhotos);

const filteredPhotos = computed(() =>
  photos.value.filter((photo) =>
    photo.title.toLowerCase().includes(searchQuery.value.toLowerCase())
  )
);
</script>

<style>
body {
  font-family: Arial, sans-serif;
  margin: 0;
  padding: 0;
}
#app {
  padding-bottom: 50px;
}
</style>
