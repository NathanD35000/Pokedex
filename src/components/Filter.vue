<script setup>
import { ref } from 'vue'

const types = ['Steel', 'Fighting', 'Dragon', 'Water', 'Electric', 'Fairy', 'Fire', 'Ice', 'Bug', 'Normal', 'Grass', 'Poison', 'Psychic', 'Rock', 'Ground', 'Ghost', 'Dark', 'Flying']
const selectedTypes = ref([])

const filterContainer = ref(null)

const toggleFilter = () => {
  filterContainer.value.classList.toggle('active')
}

defineExpose({
  selectedTypes
})
</script>
 
<template>
  <button class="filter-btn" @click="toggleFilter">
    <img src="../assets/filter.svg" alt="">
  </button>
  <div class="filter-container" ref="filterContainer">
    <div v-for="(type, i) in types" :key="i" class="type">      
      <input type="checkbox" name="" :id="type" :value="type" v-model="selectedTypes">
      <label :for="type">
        <img :src="'../assets/types/standard/' + type + '.svg'" alt="">
      </label>
    </div>
  </div>
  <div class="filter-container" ref="filterContainer">    
    <div class="filter-list">
      <div v-for="(type, i) in types" :key="i" class="checkbox-container">
        <input type="checkbox" name="" :id="type" :value="type" v-model="selectedTypes">
        <label :for="type">
          <img :src="'src/assets/types/standard/' + type.toLowerCase() + '.svg'" alt="">
        </label>
    </div>
    </div>
    <button class="filter-btn" @click="toggleFilter">Recherche avancée</button>
  </div>
</template>

<style scoped>
.filter-container {
  position: absolute;
  width: 100%;
  transform: translateY(-282px);
  transition: transform .2s ease-in-out;
  z-index: 0;
}

.filter-container.active {
  transform: translateY(0);
  z-index: 1;
}

.filter-list {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  justify-items: center;
  row-gap: 10px;
  padding: 20px 30px;
  overflow: scroll;
}

.checkbox-container {
  position: relative;
  display: flex;
  align-items: center;
  gap: 8px;
}

.checkbox-container input {
  opacity: 0;
}

.checkbox-container label::before {
  content: '';
  position: absolute;
  top: 2px;
  left: 0;
  height: 14px;
  width: 14px;
  border: 2px solid black;
  border-radius: 2px;
}

.checkbox-container label::after {
  content: none;
  position: absolute;
  top: 6px;
  left: 3px;
  height: 4px;
  width: 8px;
  border-left: 2px solid #101010;
  border-bottom: 2px solid #101010;

  transform: rotate(-45deg);
}

.checkbox-container img {
  height: 18px;
}

.checkbox-container input:checked+label::before {
  background-color: #FFF;
}

.checkbox-container input:checked+label::after {
  content: '';
}

.filter-btn {
  display: block;
  position: relative;
  height: 32px;
  width: calc(100% - 60px);
  margin-inline: auto;
  padding-right: 20px;
  background-color: #646464;
  color: white;
  font-size: 14px;
  font-weight: 500;
}

.filter-btn::after {
  content: '';
  position: absolute;
  top: 15px;
  height: 5px;
  width: 10px;
  margin-left: 10px;
  background-color: #FFF;
  clip-path: polygon(0 0, 100% 0, 50% 100%);
  transition: transform .2s ease-in-out;
}

.filter-container.active .filter-btn::after {
  transform: rotateX(180deg);
}

.filter-btn {
  left: 30px;
  bottom: 24px;
  height: 50px;
  width: 200px;
  padding-top: 5px;
  border: none;
  border-radius: 20%;
}

.filter-container {
  display: flex;
  flex-direction: column;
  gap: 10px;
  position: fixed;
  left: 30px;
  bottom: 90px;
  height: 250px;
  padding: 12px 16px;
  border: 3px solid #101010;
  border-radius: 8px;
  background-color: #F1F1F1;
  overflow: scroll;
  opacity: 0;
  transform: translateY(15px);
  transition: transform .1s ease-in-out, opacity .1s ease-in-out;
}

.filter-container.active {
  opacity: 1;
  transform: translateY(0);
}

.type {
  display: flex;
  align-items: center;
  gap: 10px;
}

label img {
  display: block;
}
</style>