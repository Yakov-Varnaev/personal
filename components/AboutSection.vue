<template>
  <section ref="container" class="about-me-horizontal">
    <div class="pinned">
      <div class="slides" :style="slideStyle">
        <div
          v-for="(event, index) in events"
          :key="index"
          class="slide"
          :style="{ background: event.background }"
        >
          <div class="slide-content">
            <v-icon
              size="80"
              class="slide-icon"
              :style="{ transform: `translateY(${scrollY * 0.1}px)` }"
            >
              {{ event.icon }}
            </v-icon>
            <h2 class="slide-year">{{ event.year }}</h2>
            <h1 class="slide-title">{{ event.title }}</h1>
            <p class="slide-description">{{ event.description }}</p>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref, onMounted, onUnmounted, computed } from "vue";

const container = ref(null);
const scrollY = ref(0);
const totalSlides = 6;

const events = [
  {
    year: "2019",
    title: "Python",
    description: "Начал писать на Python.",
    icon: "mdi-language-python",
    background: "linear-gradient(to right, #fceabb, #f8b500)",
  },
  {
    year: "2020",
    title: "Backend",
    description: "Первая работа с FastAPI.",
    icon: "mdi-server",
    background: "linear-gradient(to right, #d3cce3, #e9e4f0)",
  },
  {
    year: "2021",
    title: "Go",
    description: "Перешел на Go и микросервисы.",
    icon: "mdi-cloud-outline",
    background: "linear-gradient(to right, #00c6ff, #0072ff)",
  },
  {
    year: "2022",
    title: "CI/CD",
    description: "Настроил пайплайны.",
    icon: "mdi-cogs",
    background: "linear-gradient(to right, #f7971e, #ffd200)",
  },
  {
    year: "2023",
    title: "Лидерство",
    description: "Лидил команду.",
    icon: "mdi-account-group",
    background: "linear-gradient(to right, #9be15d, #00e3ae)",
  },
  {
    year: "2024",
    title: "Техлид",
    description: "Техлид в Яндексе.",
    icon: "mdi-star-circle",
    background: "linear-gradient(to right, #fc466b, #3f5efb)",
  },
];

const handleScroll = () => {
  if (!container.value) return;
  const rect = container.value.getBoundingClientRect();
  const offset = Math.max(-rect.top, 0);
  scrollY.value = offset;
};

onMounted(() => {
  window.addEventListener("scroll", handleScroll);
});
onUnmounted(() => {
  window.removeEventListener("scroll", handleScroll);
});

const slideStyle = computed(() => {
  const percentage = scrollY.value / (window.innerHeight * totalSlides);
  return {
    transform: `translateX(-${percentage * 100}%)`,
  };
});
</script>

<style scoped>
.about-me-horizontal {
  height: calc(100vh * 6);
  position: relative;
}

.pinned {
  position: sticky;
  top: 0;
  height: 100vh;
  overflow: hidden;
  display: flex;
  align-items: center;
}

.slides {
  display: flex;
  flex-direction: row;
  transition: transform 0.2s ease-out;
  will-change: transform;
  height: 100%;
}

.slide {
  width: 100vw;
  flex-shrink: 0;
  display: flex;
  justify-content: center;
  align-items: center;
  background-size: cover;
  background-position: center;
  position: relative;
}

.slide-content {
  text-align: center;
  padding: 40px;
  background: rgba(255, 255, 255, 0.15);
  backdrop-filter: blur(8px);
  border-radius: 24px;
  box-shadow: 0 0 40px rgba(0, 0, 0, 0.15);
  max-width: 700px;
  width: 80%;
  animation: fadeIn 1s ease;
  transition: background 0.5s;
}

.slide-icon {
  color: white;
  filter: drop-shadow(0 0 10px rgba(255, 255, 255, 0.6));
  margin-bottom: 24px;
}

.slide-year {
  font-size: 1.8rem;
  color: rgba(255, 255, 255, 0.8);
  margin-bottom: 12px;
}

.slide-title {
  font-size: 3rem;
  font-weight: 700;
  color: white;
  margin-bottom: 16px;
}

.slide-description {
  font-size: 1.25rem;
  color: rgba(255, 255, 255, 0.9);
  line-height: 1.6;
}

@keyframes fadeIn {
  from {
    opacity: 0;
    transform: translateY(30px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}
</style>
