<template>
  <section ref="container" class="about-me-stack" id="about">
    <div class="stack-wrapper">
      <div
        v-for="(event, index) in events"
        :key="index"
        class="stack-card"
        :class="{ active: index === activeIndex }"
        :style="cardStyle(index)"
      >
        <v-icon size="80" class="stack-icon">{{ event.icon }}</v-icon>
        <h2 class="stack-year">{{ event.year }}</h2>
        <h1 class="stack-title">{{ event.title }}</h1>
        <p class="stack-description">{{ event.description }}</p>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref, onMounted, onUnmounted, computed } from "vue";

const container = ref(null);
const scrollY = ref(0);

const events = [
  {
    year: "2019",
    title: "Python",
    description: "Начал писать на Python.",
    icon: "mdi-language-python",
  },
  {
    year: "2020",
    title: "Backend",
    description: "Первая работа с FastAPI.",
    icon: "mdi-server",
  },
  {
    year: "2021",
    title: "Go",
    description: "Перешел на Go и микросервисы.",
    icon: "mdi-cloud-outline",
  },
  {
    year: "2022",
    title: "CI/CD",
    description: "Настроил пайплайны.",
    icon: "mdi-cogs",
  },
  {
    year: "2023",
    title: "Лидерство",
    description: "Лидил команду.",
    icon: "mdi-account-group",
  },
  {
    year: "2024",
    title: "Техлид",
    description: "Техлид в Яндексе.",
    icon: "mdi-star-circle",
  },
];

const total = events.length;

const activeIndex = computed(() => {
  if (!container.value) return 0;

  const sectionTop = container.value.offsetTop;
  const relativeScroll = scrollY.value - sectionTop;
  const viewportHeight = window.innerHeight;

  if (relativeScroll <= 0) return 0;
  if (relativeScroll >= viewportHeight * (total - 1)) return total - 1;

  return Math.floor(relativeScroll / viewportHeight);
});

const onScroll = () => {
  scrollY.value = window.scrollY;
};

onMounted(() => {
  window.addEventListener("scroll", onScroll);
  onScroll(); // для инициализации сразу
});

onUnmounted(() => {
  window.removeEventListener("scroll", onScroll);
});
const cardStyle = (index) => {
  const offset = index - activeIndex.value;

  if (offset < 0) {
    // Карточки, которые уже были "пролистаны" — уезжают вниз и прозрачны
    return {
      transform: `translateY(40px) scale(0.9)`,
      opacity: 0,
      pointerEvents: "none",
      zIndex: 10,
      transition: "all 0.5s ease",
    };
  } else if (offset === 0) {
    // Активная карточка — на виду, крупнее
    return {
      transform: `translateY(0px) scale(1)`,
      opacity: 1,
      zIndex: 30,
      transition: "all 0.5s ease",
    };
  } else {
    // Карточки, которые впереди — сдвинуты вниз, чуть меньше, и ниже по слою
    const translateY = offset * 20;
    const scale = 1 - offset * 0.05;
    const opacity = 1 - offset * 0.3;
    return {
      transform: `translateY(${translateY}px) scale(${scale})`,
      opacity: opacity,
      zIndex: 20 - offset,
      transition: "all 0.5s ease",
      pointerEvents: "none",
    };
  }
};
</script>

<style scoped>
/* .about-section { */
/*   padding: 96px 0; */
/*   color: white; */
/*   transition: background 0.6s ease; */
/* } */

.about-me-stack {
  height: calc(100vh * 6);
  position: relative;
  background: linear-gradient(to bottom, #2c5364 0%, #39597a 100%);
}

.stack-wrapper {
  position: sticky;
  top: 0;
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  color: white;
}

.stack-card {
  position: absolute;
  width: 80%;
  max-width: 800px;
  background: rgba(255, 255, 255, 0.07);
  backdrop-filter: blur(10px);
  border-radius: 24px;
  padding: 40px;
  box-shadow: 0 20px 40px rgba(0, 0, 0, 0.25);
  user-select: none;
}
.stack-icon {
  margin-bottom: 20px;
  filter: drop-shadow(0 0 8px rgba(255, 255, 255, 0.6));
}

.stack-year {
  font-size: 1.4rem;
  opacity: 0.8;
  margin-bottom: 8px;
}

.stack-title {
  font-size: 2.5rem;
  font-weight: 700;
  margin-bottom: 16px;
}

.stack-description {
  font-size: 1.2rem;
  line-height: 1.6;
  opacity: 0.95;
}
</style>
