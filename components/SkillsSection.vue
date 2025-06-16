<template>
  <section class="skills-section">
    <div class="title-block">
      <h2 class="title">Skills</h2>
      <p class="subtitle">Технологии с которыми я могу помочь</p>
    </div>
    <div
      class="auto-slider"
      @mouseenter="pauseScroll"
      @mouseleave="resumeScroll"
    >
      <div class="slider-track" ref="track">
        <div
          v-for="(skill, index) in duplicatedSkills"
          :key="index"
          class="slide"
        >
          <div class="skill-card">
            <v-icon size="36" class="icon" :style="{ color: skill.color }">
              {{ skill.icon }}
            </v-icon>
            <div class="skill-name">{{ skill.name }}</div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from "vue";

const skills = [
  { name: "Python", icon: "mdi-language-python", color: "#FFD343" },
  { name: "Golang", icon: "mdi-language-go", color: "#00ADD8" },
  { name: "FastAPI", icon: "mdi-lightning-bolt-outline", color: "#20C997" },
  { name: "PostgreSQL", icon: "mdi-database", color: "#336791" },
  { name: "Kafka", icon: "mdi-transmission-tower", color: "#000000" },
  { name: "Docker", icon: "mdi-docker", color: "#2496ED" },
  { name: "Kubernetes", icon: "mdi-kubernetes", color: "#326CE5" },
  { name: "Redis", icon: "mdi-database-outline", color: "#DC382D" },
];

const duplicatedSkills = [...skills, ...skills];

const track = ref(null);
let animationFrame;
let isPaused = false;

const scroll = () => {
  if (!track.value || isPaused) return;

  track.value.scrollLeft += 0.7;

  const halfScroll = track.value.scrollWidth / 2;
  if (track.value.scrollLeft >= halfScroll) {
    track.value.scrollLeft -= halfScroll;
  }

  animationFrame = requestAnimationFrame(scroll);
};

const pauseScroll = () => {
  isPaused = true;
};

const resumeScroll = () => {
  if (!isPaused) return;
  isPaused = false;
  animationFrame = requestAnimationFrame(scroll);
};

onMounted(() => {
  animationFrame = requestAnimationFrame(scroll);
});

onUnmounted(() => {
  cancelAnimationFrame(animationFrame);
});
</script>

<style scoped>
.skills-section {
  padding: 80px 0;
  backdrop-filter: blur(20px);
  overflow: hidden;
  position: relative;
  color: white;
}

.title-block {
  text-align: center;
  margin-bottom: 48px;
}

.title {
  font-size: 2rem;
  font-weight: 700;
}

.subtitle {
  font-size: 1.125rem;
  color: rgba(255, 255, 255, 0.75);
}

.auto-slider {
  overflow: hidden;
  width: 100%;
  padding: 16px 0;
}

.slider-track {
  display: flex;
  flex-wrap: nowrap;
  gap: 16px;
  padding: 32px 64px;
  overflow-x: scroll;
  scrollbar-width: none;
  scroll-behavior: smooth;
  -webkit-overflow-scrolling: touch;
}
.slider-track::-webkit-scrollbar {
  display: none;
}

.slide {
  flex: 0 0 auto;
}

.skill-card {
  width: 180px;
  height: 140px;
  background: rgba(255, 255, 255, 0.08);
  backdrop-filter: blur(16px);
  border-radius: 20px;
  padding: 24px;
  box-shadow: 0 8px 24px rgba(0, 0, 0, 0.2);
  transition: all 0.4s ease;
  cursor: pointer;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  text-align: center;
}

.skill-card:hover {
  transform: translateY(-4px);
  box-shadow: 0 12px 32px rgba(0, 0, 0, 0.3);
}

.icon {
  font-size: 2rem;
  margin-bottom: 8px;
}

.skill-name {
  font-size: 1rem;
  font-weight: 500;
  color: rgba(255, 255, 255, 0.85);
}

/* Dark mode override */
:deep(.v-theme--dark) .skill-card {
  background: rgba(30, 30, 30, 0.85);
  backdrop-filter: blur(20px);
  color: rgba(255, 255, 255, 0.9);
}
</style>
