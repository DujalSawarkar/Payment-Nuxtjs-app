<template>
  <div class="bg-white shadow-2xl rounded px-8 pt-6 pb-8 mb-4 w-[80%]">
    <form @submit.prevent="submitForm">
      <div class="mb-4">
        <label class="block text-gray-700 text-lg font-bold mb-2" for="name">
          Name of User
        </label>
        <el-select
          v-model="username"
          filterable
          allow-create
          default-first-option
          :reserve-keyword="false"
          placeholder="Choose tags for your article"
          style="width: 360px"
        >
          <el-option
            v-for="item in options"
            :key="item.value"
            :label="item.label"
            :value="item.value"
          />
        </el-select>
      </div>
      <div class="mb-4">
        <label
          class="block text-gray-700 text-lg font-bold mb-2"
          for="description"
        >
          Payment Detail
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
        <label class="block text-gray-700 text-lg font-bold mb-2" for="amount">
          Amount of Transaction
        </label>
        <el-input
          v-model="amount"
          class="appearance-none rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
          placeholder="Please input Amount of Transaction"
        />
      </div>

      <div class="flex items-center justify-between ml-2">
        <button
          type="submit"
          class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline"
        >
          Submit
        </button>
      </div>
    </form>
  </div>
</template>

<script lang="ts" setup>
import { ref, onMounted } from "vue";

const username = ref<string[]>([]);
const amount = ref("");
const description = ref("");
const options = ref([]);
let user: any;

onMounted(async () => {
  user = localStorage.getItem("userData");
  await fetchUserData();
});

const fetchUserData = async () => {
  try {
    const response = await fetch("http://localhost:4000/user/all", {
      method: "GET",
      headers: {
        Authorization: `Bearer ${user}`,
      },
    });

    if (!response) {
      throw new Error("Failed to fetch user data");
    }

    const userData = await response.json();
    options.value = userData.map((user: any) => ({
      value: user.id.toString(),
      label: user.name,
    }));
  } catch (error) {
    console.error("Error fetching user data:", error);
  }
};

const submitForm = async () => {
  const formData = {
    amount: amount.value,
    name: username.value,
    description: description.value,
  };

  try {
    const response = await $fetch("http://localhost:4000/transaction/payment", {
      method: "POST",
      headers: {
        "Content-Type": "application/json",
        Authorization: `Bearer ${user}`,
      },
      body: formData,
    });

    if (!response) {
      throw new Error("Failed to submit form data");
    }

    console.log("Form data submitted successfully!");
    // Reset form fields if needed
  } catch (error) {
    console.error("Error submitting form data:", error);
  }
};
</script>
