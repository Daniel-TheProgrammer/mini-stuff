<template>
  <div class="box">
      <div v-for="(item, index) in items" :key="index">
        <div v-for="(subItem, subIndex) in item" :key="subIndex" class="square">
          {{ subItem }}
        </div>
      </div>
  </div>
</template>

<script setup lang="ts">
import { ref, onMounted } from 'vue'

const items = ref<number[][]>([])

const generateLists = () => {
  const newItems: number[][] = []
  const numberOfVerticalLists = Math.floor(Math.random() * 100) + 1
  for (let i = 0; i < numberOfVerticalLists; i++) {
    const horizontalList: number[] = []
    const numberOfItems = 10
    for (let j = 0; j < numberOfItems; j++) {
      horizontalList.push(Math.floor(Math.random() * 100) + 10)
    }
    newItems.push(horizontalList)
  }
  items.value = newItems
}

const updateRandomNumber = () => {
  const randomVerticalIndex = Math.floor(Math.random() * items.value.length)
  const randomHorizontalIndex = Math.floor(Math.random() * items.value[randomVerticalIndex].length)
  items.value[randomVerticalIndex][randomHorizontalIndex] = Math.floor(Math.random() * 100)
}

onMounted(() => {
  generateLists()
  setInterval(updateRandomNumber, 1000)
})
</script>

<style scoped>
.box {
  display: 'flex';
  justify-content: center;
}
.square {
  width: 50px;
  text-align: center;
  line-height: 50px;
  cursor: pointer;
  height: 50px;
  border: 1px solid #000;
  border-radius: 10px;
  display: inline-block;
  margin: 5px;
  transition: all 0.3s ease;
}

.square:hover {
  transform: scale(0.8);
}
</style>
