<script setup>
defineProps({
  pokemon: Object,
  completeId: Function,
  display: String
})
</script>

<template>
  <li :class="{ card: true, grid: display === 'grid', list: display === 'list' }">
    <div v-if="display === 'grid'" class="container">
      <img class="pokeimage" :src="'assets/thumbnails/' + completeId(pokemon.id) + '.png'" alt="">
      <span class="id">{{ 'N° ' + completeId(pokemon.id) }}</span>
      <div class="type">
        <img class="poketype" v-for="pokemonType in pokemon.type" :src="'src/assets/types/icon/' + pokemonType.toLowerCase() + '.svg'" alt="">
      </div>
    </div>
    <span v-if="display === 'grid'" class="name">{{ pokemon.name.french }}</span>

    <img v-if="display === 'list'" :src="'../assets/sprites/' + completeId(pokemon.id) + 'MS.png'" alt="">
    <span v-if="display === 'list'">{{ pokemon.name.french }}</span>
    <div v-if="display === 'list'" class="type">
      <img v-for="pokemonType in pokemon.type" :src="'../assets/types/standard/' + pokemonType.toLowerCase() + '.svg'" alt="">
    </div>
  </li>
</template>

<style scoped>
.card.list {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  align-items: center;
  padding: 4px 10px 4px 2px;
  border-radius: 8px;
  background-color: #F1F1F1;
  cursor: pointer;
}

.card.list .type {
  display: flex;
  flex-direction: column;
  gap: 4px;
}

.card.grid {
  position: relative;
  width: 150px;
  font-weight: 500;
  cursor: pointer;
}

.container {
  position: relative;
  padding: 25px;
  border-radius: 12px;
  border-style: solid;
  border-color: #F1F1F1;
}

.id {
  position: absolute;
  left: 10px;
  bottom: 3px;
  font-size: 12px;
  color: white;
}

.card.grid .type {
  position: absolute;
  right: 4px;
  bottom: 4px;
  display: flex;
  gap: 2px;
}

.name {
  display: block;
  margin-top: 3px;
  margin-left: 10px;  
  color: white;
}

.pokeimage{
  width: 40px;
  height: 40px;
}

.poketype{
  width: 25px;
  height: 25px;
}

</style>