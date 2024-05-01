<template>
  <div class="box">
    <div v-for="(item, index) in items" :key="index">
      <div
        v-for="(subItem, subIndex) in item"
        :key="subIndex"
        :class="{ square: true, updated: subItem.updated }"
      >
        {{ subItem.updated ? subItem.number : subItem.number }}
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref, onMounted } from 'vue'

const items = ref<{ number: number; updated: Boolean }[][]>([])

const generateLists = () => {
  const newItems: { number: number; updated: Boolean }[][] = []
  const numberOfVerticalLists = Math.floor(Math.random() * 100) + 1
  for (let i = 0; i < numberOfVerticalLists; i++) {
    const horizontalList: { number: number; updated: boolean }[] = []
    const numberOfItems = 10
    for (let j = 0; j < numberOfItems; j++) {
      horizontalList.push({
        number: Math.floor(Math.random() * 100) + 20,
        updated: false
      })
    }
    newItems.push(horizontalList)
  }
  items.value = newItems
}
const updateRandomNumber = () => {
  const randomVerticalIndex = Math.floor(Math.random() * 15)
  const randomHorizontalIndex = Math.floor(Math.random() * 10)
  if (items.value[randomVerticalIndex][randomHorizontalIndex].updated === true) {
    return
  }
  items.value[randomVerticalIndex][randomHorizontalIndex] = {
    number: Math.floor(Math.random() * 100) + 20,
    updated: true
  }
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
.updated {
  background-color: rgba(0, 255, 0, 0.5);
}
</style>