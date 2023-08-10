<template>
  <header class="sticky top-0 bg-white shadow-lg z-10">
    <nav
      class="container flex flex-col sm:flex-row items-center gap-4 text-black py-3"
    >
      <RouterLink :to="{ name: 'home' }">
        <div class="flex items-center gap-3">
          <p class="text-2xl flex"><img src="https://res.cloudinary.com/dzxbbqq4l/image/upload/v1691668906/Silky_Systems_Logo.png" alt="logo skilly systems" class="w-[170px]"> <span class="flex self-center">Weather App</span> </p>
        </div>
      </RouterLink>

      <div class="flex gap-3 flex-1 justify-end">
        <i
          class="fa-solid to fa-plus text-xl hover:text-weather-secondary duration-150 cursor-pointer"
          @click="addCity"
        ></i>
      </div>
    </nav>
  </header>
</template>

<script setup>
import { RouterLink, useRoute, useRouter } from "vue-router";
import { uid } from "uid";
import { ref } from "vue";

const savedCities = ref([]);
const locc = ref(true);
const route = useRoute();
const router = useRouter();
const addCity = () => {
if (window.location.pathname === '/'){
  alert('Hello Ahamed Riham, Please Use "+" only in weather view page to save it in localstorage & i know & can display it none')
}else {
  if (localStorage.getItem("savedCities")) {
    savedCities.value = JSON.parse(
      localStorage.getItem("savedCities")
    );
  }

  const locationObj = {
    id: uid(),
    state: route.params.state,
    city: route.params.city,
    coords: {
      lat: route.query.lat,
      lng: route.query.lng,
    },
  };

  savedCities.value.push(locationObj);
  localStorage.setItem(
    "savedCities",
    JSON.stringify(savedCities.value)
  );

  let query = Object.assign({}, route.query);
  delete query.preview;
  query.id = locationObj.id;
  router.replace({ query });
}
};
</script>
