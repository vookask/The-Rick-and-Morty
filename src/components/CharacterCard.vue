<template>
  <div class="card">
    <img
      :src="character.image"
      :alt="character.name"      
    />
    <div class="card__desc">
      <h2 class="card__name">{{ character.name }}</h2>
      <h3 class="">
        <span class="card__status">{{ character.status }}-</span>
        <span class="card__species">{{ character.species }}</span>
      </h3>
      <div class="text-gray">Last known location:</div>
      <div class="card__origin">{{ character.origin.name }}</div>
      <div class="text-gray">First seen in:</div>
      <div class="card__location">{{ character.location.name }}</div>
    </div>
  </div>
</template>

<script setup>
import { defineProps } from "vue";
defineProps({
  character: Object,
});
</script>
