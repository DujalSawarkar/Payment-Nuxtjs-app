<template>
  <el-select
    v-model="value"
    filterable
    placeholder="Select"
    style="width: 240px"
    @change="changeinput()"
  >
    <el-option
      v-for="item in options"
      :key="item.value"
      :label="item.label"
      :value="item.value"
    />
  </el-select>
</template>

<script lang="ts" setup>
import { ref, defineProps } from "vue";

// Define props
const props = defineProps({
  initialOptions: {
    type: Array,
    required: true,
  },
});

const changeinput = () => {
  const compvalue: any = value.value;
  console.log(compvalue);
};

const value = ref<string[]>([]);
// console.log(value);

const options = ref(props.initialOptions);
console.log(options.value);
</script>
