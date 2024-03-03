<template>
  <div class="bg-white shadow-2xl rounded px-8 pt-6 pb-8 mb-4">
    <div class="mb-4">
      <label class="block text-gray-700 text-sm font-bold mb-2" for="name">
        Name of Transaction
      </label>
      <el-input
        v-model="name"
        class="appearance-none rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
        placeholder="Please input Name of Transaction"
      />
    </div>
    <div class="mb-4">
      <label
        class="block text-gray-700 text-sm font-bold mb-2"
        for="description"
      >
        Description
      </label>
      <el-input
        v-model="description"
        class="appearance-none rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
        :rows="2"
        type="textarea"
        placeholder="Please input Description"
      />
    </div>
    <div class="mb-6">
      <label class="block text-gray-700 text-sm font-bold mb-2" for="amount">
        Amount of Transaction
      </label>
      <el-input
        v-model="amount"
        class="appearance-none rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
        placeholder="Please input Amount of Transaction"
      />
    </div>
    <div class="flex items-center justify-between">
      <button
        @click="submitForm"
        class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline"
      >
        Submit
      </button>
    </div>
  </div>
</template>

<script lang="ts" setup>
import { ref } from "vue";
const router = useRouter();
let user;
const name = ref("");
const amount = ref("");
const description = ref("");

onMounted(() => {
  user = localStorage.getItem("userData");
});
const submitForm = async () => {
  const formData = {
    name: name.value,
    amount: amount.value,
    description: description.value,
  };
  try {
    const response = await $fetch("http://localhost:4000/transaction", {
      method: "POST",
      headers: { Authorization: `Bearer ${user}` },
      body: formData,
    });

    if (!response) {
      throw new Error("Network response was not ok");
    }

    console.log("Transaction submitted successfully!");
    // Handle success response if needed
  } catch (error) {
    console.error("Error submitting transaction:", error);
    // Handle error appropriately
  }
  console.log(formData);
};
</script>
