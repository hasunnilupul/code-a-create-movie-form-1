<script setup>
import { ref } from "vue";
import { StarIcon } from "@heroicons/vue/24/solid";

import CreateMovieModal from "@/components/CreateMovieModal.vue";
import { items } from "./movies.json";
const movies = ref(items);
const showModal = ref(false);

function updateRating(movieIndex, rating) {
  movies.value[movieIndex].rating = rating;
}

const addMovie = (event) => {
  movies.value = movies.value.concat(event);
  showModal.value = false;
};
</script>

<template>
  <div class="app">
    <div class="header">
      <button class="primary-button" @click="showModal = !showModal">Add Movie</button>
    </div>
    <div class="movie-list">
      <div class="movie-item" v-for="(movie, movieIndex) in movies" :key="movie.id">
        <div class="movie-item-image-wrapper">
          <div class="movie-item-star-wrapper">
            <StarIcon
              id="rating"
              class="movie-item-star-rating-icon"
              :class="[movie.rating ? 'text-yellow-500' : 'text-gray-500']"
            />
            <div class="movie-item-star-content-wrapper">
              <span
                v-if="movie.rating"
                id="rating-stars"
                class="movie-item-star-content-rating-rated"
              >
                {{ movie.rating }}
              </span>
              <span v-else class="movie-item-star-content-rating-not-rated"> - </span>
            </div>
          </div>
          <img :src="movie.image" class="movie-item-image" alt="" />
        </div>

        <div class="movie-item-content-wrapper">
          <div class="movie-item-title-wrapper">
            <h3 class="movie-item-title">{{ movie.name }}</h3>
            <div class="movie-item-genres-wrapper">
              <span
                v-for="genre in movie.genres"
                :key="`${movie.id}-${genre}`"
                class="movie-item-genre-tag"
                >{{ genre }}</span
              >
            </div>
          </div>
          <div class="movie-item-description-wrapper">
            <p class="movie-item-description">{{ movie.description }}</p>
          </div>
          <div class="movie-item-rating-wrapper">
            <span class="movie-item-rating-text"> Rating: ({{ movie.rating }}/5) </span>

            <div class="movie-item-star-icon-wrapper">
              <button
                v-for="star in 5"
                :key="star"
                class="movie-item-star-icon-button"
                :class="[star <= movie.rating ? 'text-yellow-500' : 'text-gray-500']"
                :disabled="star === movie.rating"
                @click="updateRating(movieIndex, star)"
              >
                <StarIcon class="movie-item-star-icon" />
              </button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
  <create-movie-modal
    v-if="showModal"
    @close="showModal = false"
    @submit="addMovie($event)"
  />
</template>
