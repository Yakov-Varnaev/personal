<template>
  <v-app>
    <v-app-bar app flat :class="[{ 'elevated-header': scrolled }, 'px-6']">
      <v-toolbar-title class="font-weight-bold text-h6"
        >Яков Варнаев</v-toolbar-title
      >
      <v-spacer />
      <div class="d-none d-sm-flex align-center">
        <NavButton to="#about" text="Обо мне" />
        <NavButton to="#projects" text="Проекты" />
        <NavButton to="#skills" text="Навыки" />
        <NavButton to="#contact" text="Контакты" />
      </div>
    </v-app-bar>

    <v-main>
      <slot />
    </v-main>
  </v-app>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from "vue";
import NavButton from "~/components/NavButton.vue";

const scrolled = ref(false);

const handleScroll = () => {
  scrolled.value = window.scrollY > 20;
};

onMounted(() => {
  window.addEventListener("scroll", handleScroll);
});

onUnmounted(() => {
  window.removeEventListener("scroll", handleScroll);
});
</script>

<style scoped>
.elevated-header {
  background: linear-gradient(
    to bottom,
    rgba(255, 255, 255, 0.9),
    rgba(255, 255, 255, 0.7)
  );
  backdrop-filter: blur(8px);
  transition:
    background 0.3s ease,
    box-shadow 0.3s ease;
  box-shadow: 0 2px 6px rgba(0, 0, 0, 0.05);
}
</style>
