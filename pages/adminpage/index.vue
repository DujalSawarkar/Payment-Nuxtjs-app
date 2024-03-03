<template>
  <div class="p-4">
    <h1 class="text-2xl font-semibold mb-4">Admin Dashboard</h1>
    <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4">
      <div
        v-for="(user, index) in users"
        :key="index"
        class="bg-white rounded-lg shadow-md p-4"
      >
        <h2 class="text-lg font-semibold mb-2">{{ user.name }}</h2>
        <p class="text-gray-600 mb-2">Balance: ${{ user.balance }}</p>
        <button
          @click="openAddMoneyModal(user)"
          class="bg-blue-500 text-white font-semibold py-2 px-4 rounded-md shadow-md hover:bg-blue-600 focus:outline-none focus:ring focus:ring-blue-300"
        >
          Add Money
        </button>
      </div>
    </div>

    <!-- Add Money Modal -->
    <div
      v-if="showAddMoneyModal"
      class="fixed inset-0 flex items-center justify-center bg-gray-900 bg-opacity-50"
    >
      <div class="bg-white rounded-lg p-8">
        <h2 class="text-lg font-semibold mb-4">
          Add Money to {{ selectedUser.name }}
        </h2>
        <input
          v-model="amountToAdd"
          type="number"
          class="border border-gray-300 rounded-md px-4 py-2 mb-4 w-full"
          placeholder="Enter amount"
        />
        <div class="flex justify-end">
          <button
            @click="addMoney"
            class="bg-blue-500 text-white font-semibold py-2 px-4 rounded-md shadow-md hover:bg-blue-600 mr-2"
          >
            Add
          </button>
          <button
            @click="closeAddMoneyModal"
            class="bg-gray-300 text-gray-800 font-semibold py-2 px-4 rounded-md shadow-md hover:bg-gray-400"
          >
            Cancel
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref } from "vue";

interface User {
  name: string;
  balance: number;
}

const users: User[] = [
  { name: "User 1", balance: 1000 },
  { name: "User 2", balance: 2000 },
  { name: "User 3", balance: 3000 },
];

const showAddMoneyModal = ref(false);
const selectedUser = ref<User | null>(null);
const amountToAdd = ref(0);

const openAddMoneyModal = (user: User) => {
  selectedUser.value = user;
  showAddMoneyModal.value = true;
};

const closeAddMoneyModal = () => {
  showAddMoneyModal.value = false;
  amountToAdd.value = 0;
};

const addMoney = () => {
  if (selectedUser.value && amountToAdd.value > 0) {
    selectedUser.value.balance += amountToAdd.value;
    closeAddMoneyModal();
  }
};
</script>
