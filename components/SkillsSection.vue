<template>
  <section class="skills-section" id="skills">
    <div
      class="auto-slider"
      @mouseenter="pauseScroll"
      @mouseleave="resumeScroll"
    >
      <div class="slider-track" ref="track">
        <div
          class="slide"
          v-for="(skill, index) in duplicatedSkills"
          :key="index"
        >
          <v-card
            class="skill-card d-flex flex-column align-center justify-center"
            elevation="6"
            width="180"
            height="140"
          >
            <v-icon size="40" class="mb-2">{{ skill.icon }}</v-icon>
            <div class="text-subtitle-2 font-weight-medium">
              {{ skill.name }}
            </div>
          </v-card>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from "vue";

const skills = [
  { name: "Python", icon: "mdi-language-python" },
  { name: "Golang", icon: "mdi-language-go" },
  { name: "FastAPI", icon: "mdi-lightning-bolt-outline" },
  { name: "PostgreSQL", icon: "mdi-database" },
  { name: "Kafka", icon: "mdi-transmission-tower" },
  { name: "Docker", icon: "mdi-docker" },
  { name: "Kubernetes", icon: "mdi-kubernetes" },
  { name: "Redis", icon: "mdi-database-outline" },
];

// Дублируем 1 раз, чтобы был запас для плавного перехода
const duplicatedSkills = [...skills, ...skills];

const track = ref(null);
let animationFrame;
let isPaused = false;
let scrollSpeed = 0.7;

const isScrolling = ref(false);

const scroll = () => {
  if (!track.value || isPaused) {
    isScrolling.value = false;
    return;
  }

  isScrolling.value = true;
  track.value.scrollLeft += scrollSpeed;

  const scrollWidth = track.value.scrollWidth / 2;
  if (track.value.scrollLeft >= scrollWidth) {
    track.value.style.scrollBehavior = "auto";
    track.value.scrollLeft -= scrollWidth;
    requestAnimationFrame(() => {
      if (track.value) track.value.style.scrollBehavior = "smooth";
    });
  }

  animationFrame = requestAnimationFrame(scroll);
};

const pauseScroll = () => {
  isPaused = true;
};

const resumeScroll = () => {
  isPaused = false;
  if (!isScrolling.value) {
    scroll();
  }
};

onMounted(() => {
  if (track.value) {
    track.value.scrollLeft = 0;
    track.value.style.scrollBehavior = "smooth";
    animationFrame = requestAnimationFrame(scroll);
  }
});

onUnmounted(() => cancelAnimationFrame(animationFrame));
</script>

<style scoped>
.auto-slider {
  overflow: hidden;
  width: 100%;
  padding: 32px 0;
}

.slider-track {
  display: flex;
  flex-wrap: nowrap;
  gap: 16px;
  padding: 24px 64px;
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
  background: linear-gradient(
    135deg,
    rgba(255, 255, 255, 0.85),
    rgba(240, 240, 240, 0.7)
  );
  backdrop-filter: blur(8px);
  border-radius: 20px;
  box-shadow: 0 8px 24px rgba(0, 0, 0, 0.12);
  transition:
    transform 0.3s ease,
    box-shadow 0.3s ease;
  color: #333;
}

.skill-card:hover {
  transform: translateY(-6px);
  box-shadow: 0 16px 40px rgba(0, 0, 0, 0.2);
}

/* Dark theme */
:deep(.v-theme--dark) .skill-card {
  background: linear-gradient(
    135deg,
    rgba(30, 30, 30, 0.9),
    rgba(50, 50, 50, 0.65)
  );
  color: #eee;
  box-shadow: 0 8px 24px rgba(0, 0, 0, 0.6);
}
:deep(.v-theme--dark) .skill-card:hover {
  box-shadow: 0 16px 40px rgba(0, 0, 0, 0.8);
}

.skills-section {
  padding: 64px 0;
  background: linear-gradient(to bottom, #203a43 0%, #2c5364 100%);
  transition: background 0.6s ease;
  color: white;
}

:deep(.v-theme--light) .skills-section {
  background: linear-gradient(to bottom, #c3cfe2, #f5f7fa);
  color: #222;
}

.auto-slider {
  overflow: hidden;
  width: 100%;
  padding: 32px 0;
}
</style>
