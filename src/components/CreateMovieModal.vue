<script setup>
import { reactive } from "vue";

const emit = defineEmits(["close", "submit"]);

const form = reactive({
  name: "",
  description: "",
  image: "",
  genres: [],
  rating: 0,
  inTheaters: false,
});

const handleFormSubmit = () => {
  emit("submit", form);
};
</script>

<template>
  <!-- Add New Movie -->
  <div class="fixed z-30 flex items-center justify-center w-full h-full bg-gray-900/70">
    <div class="flex flex-col w-1/2 h-auto bg-gray-800 rounded p-2">
      <form class="space-y-2" @submit.prevent="handleFormSubmit">
        <div class="col-span-full">
          <label for="name" class="block text-sm font-medium leading-6 text-white"
            >Name</label
          >
          <div class="mt-2">
            <input
              type="text"
              v-model.lazy="form.name"
              id="name"
              required
              autocomplete="movie-name"
              class="block w-full rounded-md border-0 py-1.5 bg-gray-900 text-white shadow-sm ring-1 ring-inset ring-gray-500 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
            />
          </div>
        </div>

        <div class="col-span-full">
          <label for="description" class="block text-sm font-medium leading-6 text-white"
            >Description</label
          >
          <div class="mt-1.5">
            <textarea
              id="description"
              v-model.lazy="form.description"
              rows="3"
              class="block w-full rounded-md border-0 py-1.5 bg-gray-900 text-white shadow-sm ring-1 ring-inset ring-gray-500 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
            ></textarea>
          </div>
        </div>

        <div class="col-span-full">
          <label for="image" class="block text-sm font-medium leading-6 text-white"
            >Image</label
          >
          <div class="mt-1.5">
            <input
              type="text"
              v-model.lazy="form.image"
              id="image"
              autocomplete="movie-image"
              class="block w-full rounded-md border-0 py-1.5 bg-gray-900 text-white shadow-sm ring-1 ring-inset ring-gray-500 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
            />
          </div>
        </div>

        <div class="col-span-full">
          <label for="genres" class="block text-sm font-medium leading-6 text-white"
            >Genres</label
          >
          <div class="mt-2">
            <select
              id="genres"
              v-model.lazy="form.genres"
              autocomplete="genres"
              required
              class="block w-full rounded-md border-0 py-1.5 bg-gray-900 text-white shadow-sm ring-1 ring-inset ring-gray-500 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:max-w-xs sm:text-sm sm:leading-6"
              multiple
            >
              <option>Drama</option>
              <option>Action</option>
              <option>Crime</option>
              <option>Comedy</option>
              <option>Horror</option>
            </select>
          </div>
        </div>

        <div class="col-span-full flex gap-x-3 pt-1.5">
          <div class="flex h-6 items-center">
            <input
              id="in-theaters"
              v-model.lazy="form.inTheaters"
              type="checkbox"
              class="h-3 w-3 rounded border-gray-500 bg-gray-900 text-indigo-600 focus:ring-indigo-600"
            />
          </div>
          <div class="text-sm leading-6">
            <label for="in-theaters" class="font-medium text-white">In theaters</label>
          </div>
        </div>

        <div class="flex flex-row items-center justify-between pt-8">
          <button class="secondary-button" type="reset" @click="emit('close')">Cancel</button>
          <button class="primary-button" type="submit">Create</button>
        </div>
      </form>
    </div>
  </div>
</template>
