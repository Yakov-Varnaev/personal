<template>
  <v-btn
    variant="text"
    :href="to"
    class="text-caption mx-2"
    color="primary"
    style="text-transform: none"
  >
    {{ text }}
  </v-btn>
</template>

<script setup>
defineProps({
  to: String,
  text: String,
});
</script>
