<template>
  <main class="container">
    <div class="pt-4 mb-8 relative">
      <input v-model="searchQuery"
             class="py-2 px-1 bg-transparent border-b border-slate-900 w-full outline-none"
             placeholder="Search for a city or state"
             type="text"
      />
    </div>
  </main>
</template>

<script setup>
import {ref} from "vue";

const searchQuery = ref("");
</script>