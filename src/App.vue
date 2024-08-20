<script setup lang="ts">
import axios from 'axios';
import { ref, onMounted } from 'vue';

const total = ref<any[]>([]);

const getData = async () => {
  try {
    const response = await axios.get("https://rickandmortyapi.com/api/character");
    total.value = response.data.results;
  } catch (error) {
    console.error('Error fetching data:', error);
  }
};

onMounted(() => {
  getData();
});
</script>

<template>
  <div class="grid-container">
    <div v-for="(item, index) in total" :key="index" class="card">
      <img :src="item.image" alt="" class="card-image" />
      <div class="card-content">
        <h1 class="card-title">{{ item.name }}</h1>
        <p>{{ item.status }}</p>
        <p>{{ item.species }}</p>
        <p>{{ item.gender }}</p>
        <p>{{ item.origin.name }}</p>
        <p>{{ item.location.name }}</p>
        <p>Episodes: {{ item.episode.length }}</p>
      </div>
    </div>
  </div>
</template>

<style scoped>
.grid-container {
  display: grid;
  grid-template-columns: repeat(4, 1fr); 
  gap: 16px;
  padding: 16px;
}

.card {
  border: 1px solid #ddd;
  border-radius: 8px;
  overflow: hidden;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  background-color: #181818;
  display: flex;
  flex-direction: column;
}

.card-image {
  width: 100%;
  height: auto;
}

.card-content {
  padding: 16px;
}

.card-title {
  margin: 0;
  font-size: 1.5em;
}

.card p {
  margin: 4px 0;
}

@media screen and (max-width: 768px) {
  .grid-container {
    grid-template-columns: repeat(2, 1fr);
  }
}

@media screen and (max-width: 480px) {
  .grid-container {
    grid-template-columns: 1fr;
  }
} 
</style>
