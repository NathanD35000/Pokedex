<script setup>
import Card from './Card.vue'

const props = defineProps({
  filteredPokedex: Array,
  display: String,
  completeId: Function
})

const emit = defineEmits(['openModal'])

const openModal = (pokemon) => {
  emit('openModal', pokemon)
}
</script>

<template>
  <ol :class="{ pokedex: true, grid: display === 'grid', list: display === 'list' }">
    <Card v-if="filteredPokedex.length > 0" v-for="pokemon in filteredPokedex" :key="pokemon.id" :pokemon="pokemon" :completeId="completeId" :display="display" @click="openModal(pokemon)"/>
    <p class="error" v-else>Aucun pokémon ne correspond aux filtres de recherche</p>
  </ol>
</template>

<style scoped>
.pokedex {
  padding: 50px 30px;
  list-style: none;
}

.pokedex.grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
  justify-items: center;
  gap: 20px;
}

.pokedex.list {
  display: flex;
  flex-direction: column;
  gap: 12px;
  max-width: 600px;
}

.error {
  position: absolute;
  top: 50%;
  text-align: center;
  font-size: 20px;
  font-weight: 500;
  color: #888;
  transform: translateY(-50%);
}

.img{
  width: 10px;
  height: 10px;
}
</style>