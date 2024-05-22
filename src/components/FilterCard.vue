<template>
  <div class="">
    <label for="name" class="">Name:</label>
    <input type="text" id="name" v-model="name" class="" />
    <label for="status" class="">Status:</label>
    <select id="status" v-model="status" class="">
      <option value="">All</option>
      <option value="alive">Alive</option>
      <option value="dead">Dead</option>
      <option value="unknown">Unknown</option>
    </select>
    <button @click="applyFilter" class="">Apply</button>
  </div>
</template>

<script setup>
import { ref, defineEmits } from "vue";
const name = ref("");
const status = ref("");

const emit = defineEmits(["filter-applied"]);

const applyFilter = () => {
  emit("filter-applied", name.value, status.value);
};
</script>
<style scoped>
* {
  padding: 10px;
  font-size: 20px;
  color: black;
}
</style>
