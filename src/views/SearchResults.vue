<script setup>
import { ref, onMounted } from 'vue'
import { useRoute } from 'vue-router'
import { usePhotoStore } from '../stores/photos'
import PhotoModal from '../components/PhotoModal.vue';
import PhotoGrid from '../components/PhotoGrid.vue';

const route = useRoute();
const photoStore = usePhotoStore();
const query = ref(route.query.q);
const selectedPhoto = ref(null);
const isModalOpen = ref(false);


const openModal = (photo) => {
  selectedPhoto.value = photo;
  isModalOpen.value = true;
};

const closeModal = () => {
  isModalOpen.value = false;
};


onMounted(() => {
  if (query.value) {
    photoStore.getPhotosByQuery(query.value);
  }
});
</script>

<template>
  <div class="container">
    <div class="container__backdrop">
      <h1>Search Results for: {{ query }}</h1>
    </div>
    <PhotoGrid :photos="photoStore.photos" :openModal="openModal" />
    <PhotoModal :photo="selectedPhoto" :isOpen="isModalOpen" @close="closeModal" />
  </div>
</template>



