<script setup>
import { computed, ref } from 'vue';

import pokedex from './assets/pokedex.json'
import TopBar from './components/TopBar.vue'
import ToolBar from './components/ToolBar.vue'
import Filter from './components/Filter.vue'
import Pokedex from './components/Pokedex.vue'
import Modal from './components/Modal.vue'

const completeId = (id) => {
  switch (id.toString().length) {
    case 3:
      id = id.toString()
      break;
    case 2:
      id = '0' + id
      break;
    case 1:
      id = '00' + id
      break;
    default:
      break;
  }
  return id
}

const toolBar = ref(null)
const filter = ref(null)

const filteredPokedex = computed(() => {
  return pokedex.filter((pokemon) => {
    if (filter.value?.selectedTypes.length === 0)
      return pokemon.name.french.toLowerCase().includes(toolBar.value?.searchQuery.toLowerCase())
    else
      return pokemon.name.french.toLowerCase().includes(toolBar.value?.searchQuery.toLowerCase()) && filter.value?.selectedTypes.every(type => { return pokemon.type.includes(type) })
  })
})

const selectedPokemon = ref(null)
const activeModal = ref(false)

const openModal = (pokemon) => {
  selectedPokemon.value = pokemon
  activeModal.value = true
}

const closeModal = () => {
  activeModal.value = false
}

const display = ref('grid')

const setDisplay = (newDisplay) => {
  display.value = newDisplay
}
</script>

<template>
  <TopBar/>
  <ToolBar ref="toolBar" @set-display="setDisplay"/>
  <Filter ref="filter" /> 
  <Pokedex :display="display" :filteredPokedex="filteredPokedex" :completeId="completeId" @open-modal="openModal"/>
  <Modal v-if="activeModal" :selectedPokemon="selectedPokemon" :completeId="completeId" @close-modal="closeModal"/>
</template>