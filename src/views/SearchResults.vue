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
      <h1>Search Results for: <span>"{{ query }}"</span></h1>
    </div>
    <PhotoGrid class="photo-grid" :photos="photoStore.loading ? [] : photoStore.photos" :openModal="openModal" />
    <PhotoModal :photo="selectedPhoto" :isOpen="isModalOpen" @close="closeModal" />
  </div>
</template>

<style lang="scss">
h1 {
  color: $color-primary;
  font-size: 34px;
  font-weight: 600;
}
</style>