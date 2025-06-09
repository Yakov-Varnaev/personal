<template>
  <header :class="['app-header', { scrolled: isScrolled }]">
    <nav class="nav-container">
      <NuxtLink to="/" :class="['logo', { dark: isScrolled }]">
        <span class="first-name">Яков</span
        ><span class="last-name">Варнаев</span>
      </NuxtLink>
      <ul class="nav-links">
        <li><a :class="{ dark: isScrolled }" href="#about">Обо мне</a></li>
        <li><a :class="{ dark: isScrolled }" href="#skills">Навыки</a></li>
        <li><a :class="{ dark: isScrolled }" href="#review">Отзывы</a></li>
        <li><a :class="{ dark: isScrolled }" href="#contact">Контакты</a></li>
      </ul>
    </nav>
  </header>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from "vue";

const isScrolled = ref(false);

const handleScroll = () => {
  isScrolled.value = window.scrollY > 40;
};

onMounted(() => {
  window.addEventListener("scroll", handleScroll);
});

onUnmounted(() => {
  window.removeEventListener("scroll", handleScroll);
});
</script>

<style scoped>
.app-header {
  position: fixed;
  width: 100%;
  top: 0;
  z-index: 1000;
  padding: 16px 32px;
  transition:
    background-color 0.3s ease,
    box-shadow 0.3s ease;
  background: transparent;
}

.nav-container {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.logo {
  font-size: 1.4rem;
  font-weight: 700;
  font-family: "Segoe UI", "Helvetica Neue", sans-serif;
  letter-spacing: 0.5px;
  transition: color 0.3s ease;
  display: inline-flex;
  align-items: center;
  text-decoration: none;
  color: white;
}

.logo.dark {
  color: #111;
}

.logo .first-name {
  color: #2563eb; /* фиолетовый акцент */
  margin-right: 4px;
}

.logo .last-name {
  position: relative;
}

.logo .last-name::after {
  content: "";
  position: absolute;
  left: 0;
  bottom: -2px;
  width: 100%;
  height: 2px;
  background-color: currentColor;
  transform: scaleX(0);
  transition: transform 0.3s ease;
  transform-origin: left;
}

.logo:hover .last-name::after {
  transform: scaleX(1);
}

.nav-links {
  display: flex;
  gap: 24px;
  list-style: none;
}

.nav-links a {
  text-decoration: none;
  font-weight: 500;
  color: white;
  transition: color 0.3s ease;
}
.nav-links a.dark {
  color: #111;
}

.app-header.scrolled {
  background: linear-gradient(
    to bottom,
    rgba(255, 255, 255, 0.85),
    rgba(255, 255, 255, 0.6)
  );
  backdrop-filter: blur(10px);
  box-shadow: 0 2px 6px rgba(0, 0, 0, 0.08);
}

/* Dark theme fix */
:deep(.v-theme--dark) .nav-links a {
  color: white;
}
:deep(.v-theme--dark) .nav-links a.dark {
  color: #fff;
}
:deep(.v-theme--dark) .logo.dark {
  color: #fff;
}
</style>
