<script setup lang="ts">
import type { CSSProperties } from 'vue';

defineProps<{
  goalInLiters: number
  percentage: string
  percentageStyle: CSSProperties
  liters: string
  litersStyle: CSSProperties
}>()
</script>

<template>
    <h3>Goal: {{ goalInLiters }} Liters</h3>

    <div class="cup-container">
      <div class="cup">
      <div class="remained"
      :style="{ height: litersStyle.height, visibility: litersStyle.visibility }">
        <span>{{ liters }}</span>
        <small>Remained</small>
      </div>

      <div class="percentage"
      :style="{ height: percentageStyle.height, visibility: percentageStyle.visibility }">
        {{ percentage }}
      </div>
    </div>
    </div>
</template>
