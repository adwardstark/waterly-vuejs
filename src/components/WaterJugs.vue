<script setup lang="ts">
type Cup = {
  id: number
  isFull: boolean
}

defineProps<{
  cups: Array<Cup>
  quantityOfCupInML: number
}>()

const emit = defineEmits({
  onUpdate(payload: { index: number, isFull: boolean}) {
    return payload
  }
})
</script>

<template>
    <p class="text">Select how many glasses of water that you have drank</p>

    <div class="cup-container">
      <div class="cups">
      <div v-for="(cup, index) in cups" :key="cup.id">
      <div :class="[cup.isFull ? 'cup cup-small full' : 'cup cup-small']" 
        @click="emit('onUpdate', {index, isFull: !cup.isFull})"
      >
        {{ quantityOfCupInML }} ml
      </div>
      </div>
    </div>
    </div>
</template>
