<template>
  <div>
    <h1>The Rick and Morty</h1>
    <Filter @filter-applied="onFilterApplied" />
    <Pagination
      :total-pages="totalPages"
      :current-page="currentPage"
      @page-changed="onPageChanged"
    />
    <div class="section flex">
      <CharacterCard
        v-for="character in characters"
        :key="character.id"
        :character="character"
      />
    </div>
    <Pagination
      :total-pages="totalPages"
      :current-page="currentPage"
      @page-changed="onPageChanged"
    />
  </div>
</template>

<script setup>
import { ref, watch } from "vue";
import CharacterCard from "./components/CharacterCard.vue";
import Filter from "./components/FilterCard.vue";
import Pagination from "./components/PaginationCard.vue";

const currentPage = ref(1),
  filterName = ref(""),
  filterStatus = ref(""),
  characters = ref([]),
  totalPages = ref("");

watch(
  () => [currentPage.value, filterName.value, filterStatus.value],
  async () => {
    const response = await fetch(
      `https://rickandmortyapi.com/api/character?page=${currentPage.value}&name=${filterName.value}&status=${filterStatus.value}`
    );
    const data = await response.json();
    characters.value = data.results;
    totalPages.value = data.info.pages;
  },
  { immediate: true }
);

const onFilterApplied = (name, status) => {
  filterName.value = name;
  filterStatus.value = status;
};

const onPageChanged = (page) => {
  currentPage.value = page;
};
</script>
<style>
* {
  margin: 0;
  padding: 0;
}
body {
  max-width: 1920px;
  margin: 0 auto;
  text-align: center;
  font-size: 16px;
  color: rgb(245, 245, 245);
}
button {
  border: none;
  background: initial;
  cursor: pointer;
}
h1 {
  color: black;
}
.section {
  justify-content: center;
  align-items: center;
  flex-wrap: wrap;
}
.flex {
  display: flex;
}
.card {
  width: 600px;
  height: 220px;
  display: flex;
  overflow: hidden;
  background: rgb(60, 62, 68);
  border-radius: 0.5rem;
  margin: 0.75rem;
  box-shadow: rgba(0, 0, 0, 0.1) 0px 4px 6px -1px,
    rgba(0, 0, 0, 0.06) 0px 2px 4px -1px;
}
.card__img img {
  width: 100%;
  height: 100%;
  margin: 0px;
  opacity: 1;
  transition: opacity 0.5s ease 0s;
  object-position: center center;
  object-fit: cover;
}
.card__desc {
  flex: 3 1 0%;
  position: relative;
  padding: 0.75rem;
  justify-content: space-between;
  color: rgb(255, 255, 255);
  display: flex;
  flex-direction: column;
}
.text-gray {
  color: rgb(158, 158, 158);
}
</style>
