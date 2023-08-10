<template>
  <div
    class="flex flex-col min-h-screen font-Roboto bg-[url('https://res.cloudinary.com/dzxbbqq4l/image/upload/v1691683654/hero_otfb3w.jpg')] bg-cover"
  >
    <SiteNavigation />
    <RouterView class="flex-1" v-slot="{ Component }">
      <Transition name="page">
        <component :is="Component" />
      </Transition>
    </RouterView>
  </div>
</template>

<script setup>
import { RouterView } from "vue-router";
import SiteNavigation from "./components/SiteNavigation.vue";
</script>

<style>
.page-enter-active {
  transition: 600ms ease all;
}

.page-enter-from {
  opacity: 0;
}
</style>
