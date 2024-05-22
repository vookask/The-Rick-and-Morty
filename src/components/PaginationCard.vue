<template>
  <div class="flex">
    <button @click="previousPage" v-if="currentPage > 1" class="">
      Previous
    </button>
    <span class="">{{ currentPage }}</span>
    <button @click="nextPage" v-if="currentPage < totalPages" class="">
      Next
    </button>
  </div>
</template>

<script setup>
import { defineProps, defineEmits } from "vue";
const props = defineProps({
  currentPage: Number,
  totalPages: Number,
});

const emit = defineEmits(["page-changed"]);

const previousPage = () => {
  emit("page-changed", props.currentPage - 1);
};

const nextPage = () => {
  emit("page-changed", props.currentPage + 1);
};
</script>
<style scoped>
* {
  justify-content: center;
  font-size: 20px;
  color: black;
  padding: 10px;
}
</style>
