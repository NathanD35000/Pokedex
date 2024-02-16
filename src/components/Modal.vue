<script setup>
import { computed, ref } from 'vue'

import pokedex from '../assets/pokedex.json'

const emit = defineEmits([
  'closeModal'
])

const closeModal = () => {
  emit('closeModal')
}

const props = defineProps({
  selectedPokemon: Object,
  completeId: Function
})

</script>

<template>
  <div class="backdrop" @click="closeModal"></div>

  <div class="modal">
    <button class="back-btn" @click="closeModal">
      <img src="../assets/left-arrow.svg" alt="">
    </button>
    
    <div class="content-grid">
      <img class="img" :src="'../assets/thumbnails/' + completeId(selectedPokemon.id) + '.png'" alt="">
      <div>
        <p class="name">
          <span class="id">N° {{ completeId(selectedPokemon.id) }}</span>
          {{ selectedPokemon.name.french }}
        </p>
        <div class="type">
          <img v-for="pokemonType in selectedPokemon.type" :src="'../assets/types/standard/' + pokemonType.toLowerCase() + '.svg'" alt="">
        </div>
      </div>
    </div>
    
    <div class="stats-grid">
      <div class="stat">
        <span>PV</span>
        <span class="value">{{ selectedPokemon.base.HP }}</span>
      </div>
      <div class="stat">
        <span>Attaque</span>
        <span class="value">{{ selectedPokemon.base.Attack }}</span>
      </div>
      <div class="stat">
        <span>Défense</span>
        <span class="value">{{ selectedPokemon.base.Defense }}</span>
      </div>
      <div class="stat">
        <span>Atq. Spé.</span>
        <span class="value">{{ selectedPokemon.base['Sp. Attack'] }}</span>
      </div>
      <div class="stat">
        <span>Déf. Spé.</span>
        <span class="value">{{ selectedPokemon.base['Sp. Defense'] }}</span>
      </div>
      <div class="stat">
        <span>Vitesse</span>
        <span class="value">{{ selectedPokemon.base.Speed }}</span>
      </div>
    </div>
    <div>
      <button class="buttondeck">Ajouter au deck</button>
    </div>
  </div>
</template>

<style scoped>
.modal {
  position: fixed;
  top: 50%;
  left: 0;
  right: 0;
  width: calc(100vw - 60px);
  margin-inline: auto;
  padding: 16px 30px 20px;
  border-radius: 8px;
  background-color: #FFF;
  font-size: 14px;
  font-weight: 700;
  transform: translateY(-50%);
}

.buttondeck{
  align-items: center;
  color: black;
  background: none;
  border-style: solid;
  padding-top: 5px;
  padding-bottom: 5px;
  margin: 30px auto 10px auto;
  width: 5%;
  display: flex;
  justify-content: space-around;
  font-size: 15px;
  font-weight: 500;
  color: #A0A0A0;
}


.back-btn {
  display: grid;
  place-items: center;
  position: absolute;
  top: 20px;
  left: 20px;
  background-color: #FFF;
}

.content-grid {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  column-gap: 10px;
}

.img {
  justify-self: center;
  margin-top: 4px;
}

.name {
  font-size: 20px;
}

.id {
  font-size: 15px;
  font-weight: 500;
  color: #A0A0A0;
}

.type {
  margin-top: 8px;
}

.stats-grid {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 8px 10px;
  margin-top: 16px;
}

.stat {
  display: flex;
  justify-content: space-between;
  padding: 5px 8px;
  border-radius: 8px;
  background-color: #E6E6E6;
  color: #888;
}

.stat .value {
  color: #101010;
}

.backdrop {
  position: fixed;
  inset: 0;
  background-color: #101010;
  opacity: .5;
}
</style>