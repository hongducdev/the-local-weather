<template>
  <main class="container">
    <div class="pt-4 mb-8 relative">
      <input
        v-model="searchQuery"
        class="py-2 px-1 bg-transparent border-b border-slate-900 w-full outline-none"
        placeholder="Search for a city or state"
        type="text"
        @input="getSearchResult"
      />
      <ul class="absolute w-full shadow-md px-1 py-2 rounded-md top-[66px]" v-if="mapBoxSearchResult && mapBoxSearchResult.length">
        <p v-if="searchError">
          Sorry, something went wrong. Please try again later.
        </p>
        <p v-if="!searchError && mapBoxSearchResult.length == 0">
          No results found.
        </p>
        <template v-else>
          <li
            v-for="searchResult in mapBoxSearchResult"
            :key="searchResult.id"
            class="py-2 px-1 hover:bg-slate-900 hover:text-white cursor-pointer"
          >
            {{ searchResult.place_name }}
          </li>
        </template>
      </ul>
    </div>
  </main>
</template>

<script setup>
import { ref } from "vue";
import axios from "axios";

const searchQuery = ref("");
const queryTimeout = ref(null);
const mapBoxSearchResult = ref([]);
const searchError = ref(null);

const getSearchResult = () => {
  clearTimeout(queryTimeout.value);
  queryTimeout.value = setTimeout(async () => {
    if (searchQuery.value !== "") {
      try {
        const result = await axios.get(
          `https://api.mapbox.com/geocoding/v5/mapbox.places/${
            searchQuery.value
          }.json?access_token=${
            import.meta.env.VITE_MAPBOX_ACCESS_TOKEN
          }&types=place`
        );
        mapBoxSearchResult.value = result.data.features;
      } catch (error) {
        console.error("Error fetching data from MapBox API", error);
        searchError.value = true;
        mapBoxSearchResult.value = [];
      }
    } else {
      mapBoxSearchResult.value = [];
    }
  }, 300);
};
</script>
