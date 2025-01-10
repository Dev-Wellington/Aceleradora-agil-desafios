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
    const response = await fetch(
      "https://api.unsplash.com/search/photos?query=vegetables&per_page=10&client_id=SGydLV4h49lV_4crVyYEsxjaVHQLzSwO2-WZ7isVvqg"
    );
    if (!response.ok) {
      throw new Error(`Erro HTTP! Status: ${response.status}`);
    }
    const data = await response.json();
    photos.value = data.results.map(photo => ({
      id: photo.id,
      url: photo.urls.small,
      title: photo.alt_description || "Vegetable Image",
    }));
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
