<template>
  <div :style="{ color: color }">
    <div class="count">{{ count }}</div>
    <div class="label">{{ label }}</div>
  </div>
</template>

<script setup lang="ts">
defineProps<{ count: string; label: string; color?: string }>();
</script>

<style scoped>
.count {
  font-size: 4rem;
  font-weight: 800;
}
</style>
