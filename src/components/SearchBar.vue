<template>
  <div class="search-bar">
    <input
      type="text"
      v-model="searchQuery"
      placeholder="Pesquisar por nome da foto..."
    />
    <button @click="onSearch" class="search-button">🔍</button>
  </div>
</template>

<script setup>
import { ref, watch } from "vue";

const searchQuery = ref("");
const emit = defineEmits(["update:modelValue"]);

watch(searchQuery, (newValue) => {
  emit("update:modelValue", newValue);
});

const onSearch = () => {
  emit("update:modelValue", searchQuery.value);
};
</script>

<style scoped>
.search-bar {
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 0.5rem;
  margin: 1rem 0;
}

.search-bar input {
  width: 50%;
  padding: 0.5rem;
  border: 1px solid #ccc;
  border-radius: 5px;
}

.search-button {
  padding: 0.5rem 1rem;
  border: none;
  border-radius: 5px;
  background-color: #5ea507;
  color: #fff;
  cursor: pointer;
  transition: background-color 0.3s;
}

.search-button:hover {
  background-color: #518e07;
}
</style>
