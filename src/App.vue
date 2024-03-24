<script setup lang="ts">
import { ref } from 'vue';
import WaterGoal from './components/WaterGoal.vue'
import WaterJugs from './components/WaterJugs.vue'
import type { CSSProperties } from 'vue';

const goalInLiters = 2

const percentage = ref('0%')
const percentageStyle = ref({
  height: '0px',
  visibility: 'hidden'
} as CSSProperties)

const liters = ref(`${goalInLiters}L`)
const litersStyle = ref({
  height: '0px',
  visibility: 'visible'
} as CSSProperties)

const cups = ref([
  { id: 0, isFull: false },
  { id: 1, isFull: false },
  { id: 2, isFull: false },
  { id: 3, isFull: false },
  { id: 4, isFull: false },
  { id: 5, isFull: false },
  { id: 6, isFull: false },
  { id: 7, isFull: false }
])
const totalCups = cups.value.length
let fullCups = 0

const updateCups = (payload: { index: number, isFull: boolean }) => {
  cups.value[payload.index].isFull = payload.isFull
  fullCups = cups.value.filter(cup => cup.isFull).length
  updateGoal()
}

const updateGoal = () => {
  if (fullCups === 0) {
      percentage.value = ''
      percentageStyle.value = {
        height: '0px',
        visibility: 'hidden'
      }
  } else {
      percentage.value = `${fullCups / totalCups * 100}%`
      percentageStyle.value = {
        height: `${fullCups / totalCups * 330}px`,
        visibility: 'visible'
      }
    }

  if (fullCups === totalCups) {
      liters.value = ''
      litersStyle.value = {
        visibility: 'hidden',
        height: '0px'
      }
  } else {
      liters.value = `${2 - (250 * fullCups / 1000)}L`
      litersStyle.value = {
        visibility: 'visible',
        height: ''
      }
    }
}
</script>

<template>
    <h1>Waterly</h1>
    
      <WaterGoal 
        :goalInLiters="goalInLiters" 
        :liters="liters" 
        :litersStyle="litersStyle" 
        :percentage="percentage" 
        :percentageStyle="percentageStyle" />

      <WaterJugs 
        :cups="cups" 
        :quantityOfCupInML="200" 
        @onUpdate="updateCups" />
</template>

<style scoped>

</style>
