<script setup>
import { ref } from 'vue'

const searchQuery = ref('')

defineExpose({
  searchQuery
})

const listBtn = ref(null)
const gridBtn = ref(null)

const emit = defineEmits([
  'setDisplay'
])

const setDisplay = (display) => {
  if (display === 'list') {
    gridBtn.value.classList.remove('active')
    listBtn.value.classList.add('active')
  } else {
    listBtn.value.classList.remove('active')
    gridBtn.value.classList.add('active')
  }

  emit('setDisplay', display)
}
</script>

<template>
  <div class="tool-bar">
    <div class="search" ref="search">
      <div class="search-icon"/>
      <input type="search" name="" id="" placeholder="Pikachu" v-model="searchQuery" ref="input">
    </div>
    <div class="display-btns">
      <button @click="setDisplay('list')" ref="listBtn">
        <img src="../assets/inline-display-icon.svg" alt="">
      </button>
      <button class="active" @click="setDisplay('grid')" ref="gridBtn">
        <img src="../assets/grid-display-icon.svg" alt="">
      </button>
    </div>
  </div>
</template>

<style scoped>
.tool-bar {
  display: flex;
  justify-content: space-between;
  position: relative;
  padding: 12px 30px;
  z-index: 100;
}

.search {
  display: flex;
  position: relative;
  height: 36px;
  width: calc(100vw - 151px);
  max-width: 258px;
  border-radius: 8px;
  background-color: white;
}

.search:focus-within {
  outline: 2px solid #101010;
}

.search .search-icon {
  position: relative;
  top: 0px;
  left: 0px;
  height: 36px;
  width: 36px;
  border: none;
  border-radius: 8px;
  background-color: white;
  cursor: pointer;
}

.search .search-icon::before {
  content: '';
  position: absolute;
  top: 9px;
  left: 9px;
  height: 14px;
  width: 14px;
  border: 2px solid #888;
  border-radius: 50%;
}

.search .search-icon::after {
  content: '';
  position: absolute;
  top: 23px;
  left: 18px;
  height: 2px;
  width: 9px;
  border-radius: 1px;
  background-color: #888;
  transform: rotate(50deg);
}

.search input {
  height: 36px;
  width: calc(100vw - 195px);
  max-width: 214px;
  border: none;
  outline: none;
  background-color: white;
  font-family: 'Satoshi', system-ui, sans-serif;
  font-size: 16px;
  font-weight: 500;
}

.display-btns {
  display: flex;
  gap: 8px;

  button {
    display: block;
    border-radius: 8px;
    background-color: transparent;
  }

  button:not(.active) {
    opacity: .4;
  }

  button:focus-visible {
    outline: 2px solid black;
  }
}

button img {
  display: block;
}
</style>