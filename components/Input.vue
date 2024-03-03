<template>
  <el-select
    v-model="value"
    filterable
    placeholder="Select"
    style="width: 240px"
    @change="changeinput"
  >
    <el-option
      v-for="item in options"
      :key="item.value"
      :label="item.label"
      :value="item.value"
    />
  </el-select>

  <div v-if="compvalue === 'Transaction'">Transaction</div>
  <div v-else class="w-[70%] m-12"><Expenses /></div>
</template>

<script lang="ts" setup>
import { ref, defineProps } from "vue";

const props = defineProps({
  initialOptions: {
    type: Array,
    required: true,
  },
});
let compvalue = ref<string>(""); // Initialize compvalue as empty string

const changeinput = () => {
  compvalue.value = value.value; // Update compvalue directly
  console.log(compvalue.value); // Log for verification
};

const value = ref<string[]>([]);
const options = ref(props.initialOptions);
console.log(options.value); // Log options for verification
</script>
