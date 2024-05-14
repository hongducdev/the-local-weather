<template>
  <div class="flex flex-col font-poppins min-h-screen bg-slate-50 text-slate-950">
    <SiteNavigation/>
    <RouterView/>
  </div>
</template>

<script setup>
import {RouterView} from "vue-router";

import SiteNavigation from "@/components/SiteNavigation.vue";
</script>