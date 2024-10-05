<script setup>
import { defineProps } from 'vue'

const props = defineProps({
    photos: {
        type: Array,
        required: true
    },
    openModal: {
        type: Function,
        required: true
    }
})
</script>

<template>
    <div class="grid-container">
        <div v-for="photo in photos" :key="photo.id" class="grid-container__item" @click="() => openModal(photo)">
            <img :src="photo.urls.small" :alt="photo.alt_description" class="grid-container__photo-item" />
            <div class="grid-container__photo-item__info">
                <p class="grid-container__photo-item__info-name">{{ photo.user.name }}</p>
                <p class="grid-container__photo-item__info-location" v-if="photo.location">
                    {{ photo.location.name }}
                </p>
            </div>
        </div>
    </div>
</template>

<style lang="scss">
.grid-container {
    display: grid;
    gap: 16px;
    width: 100%;
    grid-template-columns: repeat(3, 1fr);
    gap: 90px;
    width: 100%;
    padding: 20px 160px;

    &__item {
        position: relative;
        cursor: pointer;
        overflow: hidden;
        border-radius: 8px;
        transition: transform 0.2s;
        border-radius: 10px;
        box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
        transition: transform 0.3s;

        &:hover {
            transform: scale(1.05);
        }

        &__photo-item {
            width: 100%;
            height: auto;
            border-radius: 8px;
        }

        &__info {
            padding: 10px;
            border-radius: 8px;
            position: absolute;
            color: #ffffff;
            bottom: 0;
            left: 0;
            right: 0;
            text-align: left;

            &-name {
                font-weight: bold;
                margin: 0;
            }

            &-location {
                margin: 0;
                font-size: 0.9em;
                color: #fff;
            }
        }
    }
}

@media (max-width: 1200px) {
    .grid-container {
        grid-template-columns: repeat(2, 1fr);
    }
}

@media (max-width: 800px) {
    .grid-container {
        grid-template-columns: 1fr;
    }
}

@media (max-width: 600px) {
    .grid-container {
        padding: 8px;

        &__item {
            &__info {
                padding: 4px;
            }
        }
    }
}
</style>