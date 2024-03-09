<template>
  <div>
    <h1>Data</h1>
    <div v-if="isLoading">Loading...</div>
    <div v-else-if="error">{{ error }}</div>
    <pre v-else>{{ data }}</pre>
  </div>
</template>

<script setup lang="ts">
import { useDataStore } from "~/store/useStore";
import { ref, onMounted } from "vue";
// if (process.client) {
//   const user = localStorage.getItem("userData");
//   console.log(user);
// }

// onMounted(() => {
//   const user = localStorage.getItem("userData"); // Set your user token here
//   console.log(user);
// });
const { data, isLoading, error } = useDataStore();
const newData = ref(null);

onMounted(async () => {
  try {
    await useDataStore.fetchData(user);
  } catch (error) {
    console.error("Error fetching data:", error);
  }
});
</script>
