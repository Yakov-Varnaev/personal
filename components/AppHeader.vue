<template>
  <header :class="['app-header', { scrolled: isScrolled }]">
    <nav class="nav-container">
      <div
        :class="['logo', { dark: isScrolled }]"
        @click="() => scrollTo('hero')"
      >
        <span class="first-name">Яков</span>
        <span class="last-name">Варнаев</span>
      </div>

      <!-- Desktop nav -->
      <ul class="nav-links">
        <li><a :class="{ dark: isScrolled }" href="#about">Обо мне</a></li>
        <li><a :class="{ dark: isScrolled }" href="#skills">Навыки</a></li>
        <li><a :class="{ dark: isScrolled }" href="#review">Отзывы</a></li>
        <li><a :class="{ dark: isScrolled }" href="#contact">Контакты</a></li>
      </ul>

      <!-- Burger button -->
      <div :class="['burger']" @click="toggleMenu">
        <span :class="{ open: isMenuOpen, dark: isScrolled }"></span>
        <span :class="{ open: isMenuOpen, dark: isScrolled }"></span>
        <span :class="{ open: isMenuOpen, dark: isScrolled }"></span>
      </div>
    </nav>

    <!-- Mobile menu -->
    <transition name="fade-slide">
      <div v-if="isMenuOpen" class="mobile-menu">
        <a href="#about" @click="closeMenu">Обо мне</a>
        <a href="#skills" @click="closeMenu">Навыки</a>
        <a href="#review" @click="closeMenu">Отзывы</a>
        <a href="#contact" @click="closeMenu">Контакты</a>
      </div>
    </transition>
  </header>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from "vue";

const isScrolled = ref(false);
const isMenuOpen = ref(false);

const toggleMenu = () => {
  isMenuOpen.value = !isMenuOpen.value;
};
const closeMenu = () => {
  isMenuOpen.value = false;
};

const handleScroll = () => {
  isScrolled.value = window.scrollY > 40;
};

const scrollTo = (id) => {
  const el = document.getElementById(id);
  if (el) {
    el.scrollIntoView({ behavior: "smooth" });
  }
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

.app-header.scrolled {
  background: linear-gradient(
    to bottom,
    rgba(255, 255, 255, 0.85),
    rgba(255, 255, 255, 0.6)
  );
  backdrop-filter: blur(10px);
  box-shadow: 0 2px 6px rgba(0, 0, 0, 0.08);
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
  cursor: pointer;
}

.logo.dark {
  color: #111;
}

.first-name {
  color: #2563eb;
  margin-right: 4px;
}

.last-name {
  position: relative;
}

.last-name::after {
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

/* Desktop nav */
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

/* Burger button */
.burger {
  display: none;
  flex-direction: column;
  gap: 5px;
  cursor: pointer;
}
.burger span {
  width: 24px;
  height: 2px;
  background: white;
  transition: 0.3s ease;
}
.burger .dark {
  background: black;
}

.burger span.open:nth-child(1) {
  transform: rotate(45deg) translate(5px, 5px);
}
.burger span.open:nth-child(2) {
  opacity: 0;
}
.burger span.open:nth-child(3) {
  transform: rotate(-45deg) translate(5px, -5px);
}

/* Mobile menu */
.mobile-menu {
  position: absolute;
  top: 100%;
  left: 0;
  width: 100%;
  background: white;
  display: flex;
  flex-direction: column;
  padding: 24px;
  gap: 16px;
  z-index: 999;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.15);
}
.mobile-menu a {
  text-decoration: none;
  font-size: 1.2rem;
  color: #111;
}

/* Transitions */
.fade-slide-enter-active,
.fade-slide-leave-active {
  transition: all 0.3s ease;
}
.fade-slide-enter-from,
.fade-slide-leave-to {
  opacity: 0;
  transform: translateY(-10px);
}

/* Responsive */
@media (max-width: 768px) {
  .nav-links {
    display: none;
  }
  .burger {
    display: flex;
  }
}
</style>
