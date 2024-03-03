<template>
  <div class="flex">
    <div
      class="h-screen w-[100%] bg-slate-100 flex justify-center items-center"
    >
      <div class="w-[90%] bg-white rounded-lg shadow-xl p-8">
        <h1 class="text-3xl font-bold mb-8">Your Expenses</h1>

        <!-- Balance and Expense section -->
        <div class="flex items-center gap-[10%] mb-12">
          <div class="flex justify-evenly items-center w-[50%]">
            <div class="flex flex-col items-center">
              <h2 class="text-2xl font-semibold text-green-500 mb-2">
                Balance
              </h2>
              <p class="text-3xl font-bold">$500</p>
            </div>
            <hr
              class="border-t border-gray-300 h-px w-20 mx-6 transform rotate-90"
            />
            <div class="flex flex-col items-center">
              <h2 class="text-2xl font-semibold text-red-500 mb-2">Expense</h2>
              <p class="text-3xl font-bold">$200</p>
            </div>
          </div>
        </div>
        <Timeline />
      </div>
    </div>
    <div class="w-full flex flex-col items-center m-12">
      <Input :initial-options="options" class="mt-4" />
    </div>
  </div>
</template>
<script setup>
const router = useRouter();
let user;
onMounted(() => {
  user = localStorage.getItem("userData");
  if (!localStorage.getItem("userData")) {
    router.push("/login");
  }
});
const options = [
  { value: "Expense", label: "Expense" },
  { value: "Transaction", label: "Transaction" },
];
</script>
