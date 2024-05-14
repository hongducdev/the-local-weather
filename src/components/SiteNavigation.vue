<script setup>
import {ref} from "vue";
import {RouterLink} from "vue-router";
import BaseModal from "@/components/BaseModal.vue";

const modalActive = ref(false);
const toggleModal = () => {
  modalActive.value = !modalActive.value;
}
</script>

<template>
  <header class="sticky top-0 shadow-md bg-slate-50">
    <nav class="container flex flex-col sm:flex-row item-center gap-4 py-6">
      <RouterLink :to="{name: 'home'}" class="text-xl md:text-2xl font-semibold text-slate-950 capitalize">the local
        weather
      </RouterLink>
      <div class="flex items-center gap-3 justify-end flex-1 text-xl hover:text-slate-700 cursor-pointer">
        <i class="fas fa-info-circle" @click="toggleModal"></i>
        <i class="fas fa-plus"></i>
      </div>

      <BaseModal :modal-active="modalActive" @close-modal="toggleModal">
        <h2 class="text-2xl font-semibold text-slate-950 mb-3">About</h2>
        <p class="mb-2">
          The Local Weather is a simple weather app that allows you to check the weather in your city.
        </p>
        <h2 class="text-2xl font-semibold text-slate-950 mb-3">How it works</h2>
        <ol class="list-decimal list-inside mb-2">
          <li>
            Search for your city by entering the city name in the search bar.
          </li>
          <li>
            Select a city within the results. This will take you to the current weather for your selection.
          </li>
          <li>
            Track the city by clicking the <i class="fas fa-plus"></i> icon in the top right. This will save the city to
            view at a later time on the home page.
          </li>
        </ol>
        <h2 class="text-2xl font-semibold text-slate-950 mb-3">Removing a city</h2>
        <p class="mb-2">
          If you no longer wish to track a city, simple select the city within the home page. At the bottom of the page,
          there will be an option to remove the city from the list.
        </p>
      </BaseModal>
    </nav>
  </header>
</template>