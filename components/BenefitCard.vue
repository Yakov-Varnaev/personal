<template>
  <v-card class="glass-card" elevation="0">
    <v-icon size="36" class="card-icon">{{ icon }}</v-icon>
    <h3 class="card-title">{{ title }}</h3>
    <p class="card-description">{{ description }}</p>
  </v-card>
</template>

<script setup lang="ts">
defineProps<{
  icon: string;
  title: string;
  description: string;
}>();
</script>

<style scoped>
.glass-card {
  backdrop-filter: blur(20px);
  background: rgba(255, 255, 255, 0.06);
  border: 1px solid rgba(255, 255, 255, 0.15);
  border-radius: 24px;
  padding: 1.5rem;
  transition: transform 0.3s ease;
  cursor: default;
  text-align: center;
  color: #fff;
  box-shadow: 0 8px 32px rgba(0, 0, 0, 0.25);
}

.glass-card:hover {
  transform: translateY(-6px);
  box-shadow: 0 12px 40px rgba(0, 0, 0, 0.35);
}

.card-icon {
  margin-bottom: 1rem;
  color: #9be6ff;
}

.card-title {
  font-size: 1.3rem;
  font-weight: 600;
  margin-bottom: 0.5rem;
}

.card-description {
  font-size: 1rem;
  opacity: 0.85;
}
</style>
