<template>
    <div class="photo-item">
      <img :src="photo.url" :alt="photo.title" />
      <h3>{{ photo.title }}</h3>
    </div>
  </template>
  
  <script setup>
  defineProps({
    photo: {
      type: Object,
      required: true,
    },
  });
  </script>
  
  <style scoped>
  .photo-item {
    text-align: center;
    transition: transform 0.3s, box-shadow 0.3s;
  }
  .photo-item img {
    width: 100%;
    height: auto;
    border-radius: 5px;
  }
  .photo-item:hover {
    transform: scale(1.05);
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
  }
  </style>
  