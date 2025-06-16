<template>
  <section class="mentorship-section" @click="closeCard">
    <v-container>
      <div class="title-block">
        <h2 class="title">Почему менторство — это важно</h2>
        <p class="subtitle">
          Рост в 2 раза быстрее. Меньше хаоса — больше уверенности.
        </p>
      </div>

      <v-row dense>
        <v-col
          v-for="(benefit, index) in benefits"
          :key="index"
          cols="12"
          sm="6"
          md="4"
        >
          <div
            class="benefit-card"
            :class="{
              expanded: expandedIndex === index,
              blurred: expandedIndex !== null && expandedIndex !== index,
            }"
            @click.stop="toggleCard(index)"
          >
            <div class="icon">{{ benefit.icon }}</div>
            <h3 class="benefit-title">{{ benefit.title }}</h3>
            <p class="benefit-description">{{ benefit.description }}</p>
            <p v-if="expandedIndex === index" class="extra-description">
              {{ benefit.extra }}
            </p>
          </div>
        </v-col>
      </v-row>

      <div class="cta">
        <button class="cta-button">Записаться на созвон</button>
      </div>
    </v-container>
  </section>
</template>

<script setup lang="ts">
import { ref } from "vue";

const expandedIndex = ref<number | null>(null);

function toggleCard(index: number) {
  expandedIndex.value = expandedIndex.value === index ? null : index;
}

function closeCard() {
  expandedIndex.value = null;
}

const benefits = [
  {
    icon: "🚀",
    title: "Быстрый рост",
    description: "Развиваешься в 2-3 раза быстрее.",
    extra:
      "Без ментора путь часто хаотичен. С наставником — ты точно знаешь следующий шаг.",
  },
  {
    icon: "🧭",
    title: "Карьерный вектор",
    description: "Фокус на нужные навыки.",
    extra:
      "Ментор помогает выстроить конкретный план и отсечь лишние действия.",
  },
  {
    icon: "🛠",
    title: "Практика, а не теория",
    description: "Решение реальных задач.",
    extra: "Ты учишься на настоящих проблемах, а не выдуманных туториалах.",
  },
  {
    icon: "💬",
    title: "Фидбек по делу",
    description: "Моментальная обратная связь.",
    extra:
      "Без догадок — тебе сразу показывают, где ошибка и как её исправить.",
  },
  {
    icon: "🔍",
    title: "Анализ слабых мест",
    description: "Увидеть то, чего сам не замечаешь.",
    extra: "Ментор подмечает паттерны и уязвимости, которые ты не осознаёшь.",
  },
  {
    icon: "🧠",
    title: "Наращивание экспертизы",
    description: "Ты перенимаешь мышление опытного разработчика.",
    extra: "Это не просто знания — это целая система принятия решений.",
  },
  {
    icon: "🤝",
    title: "Поддержка",
    description: "Плечо и опора на пути.",
    extra: "Когда сложно — ты не один. Это как мини-команда.",
  },
  {
    icon: "🎯",
    title: "Фокус и приоритеты",
    description: "Не тратишь силы впустую.",
    extra: "Ментор помогает не распыляться и делать только важное.",
  },
  {
    icon: "📈",
    title: "Траектория роста",
    description: "Ты видишь путь на 6 месяцев вперёд.",
    extra: "Становится ясно, где ты сейчас и как прийти к следующему уровню.",
  },
];

watch(expandedIndex, (newVal) => {
  if (newVal !== null) {
    document.body.classList.add("scroll-lock");
  } else {
    document.body.classList.remove("scroll-lock");
  }
});
</script>

<style scoped>
body.scroll-lock {
  overflow: hidden;
}

.mentorship-section {
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

.benefit-card {
  background: rgba(255, 255, 255, 0.08);
  border-radius: 20px;
  padding: 24px;
  box-shadow: 0 8px 24px rgba(0, 0, 0, 0.2);
  backdrop-filter: blur(16px);
  transition: all 0.4s ease;
  cursor: pointer;
  height: 100%;
  display: flex;
  flex-direction: column;
  justify-content: flex-start;
}

.benefit-card:hover {
  transform: translateY(-4px);
  box-shadow: 0 12px 32px rgba(0, 0, 0, 0.3);
}

.benefit-card.expanded {
  position: fixed;
  top: 50%;
  left: 50%;
  width: 90vw;
  max-width: 600px;
  max-height: 60vh;
  overflow-y: auto;
  z-index: 100;
  transform: translate(-50%, -50%) scale(1.05);
  box-shadow: 0 20px 40px rgba(0, 0, 0, 0.6);
  background: rgba(30, 30, 30, 0.85); /* более плотный фон */
  backdrop-filter: blur(20px);
  padding: 32px;
  border-radius: 24px;
}

.benefit-card.blurred {
  opacity: 0.3;
  pointer-events: none;
  filter: blur(2px);
  transform: scale(0.98);
}

.icon {
  font-size: 2rem;
  margin-bottom: 8px;
}

.benefit-title {
  font-size: 1.2rem;
  font-weight: 600;
}

.benefit-description {
  font-size: 1rem;
  color: rgba(255, 255, 255, 0.85);
}

.extra-description {
  margin-top: 16px;
  font-size: 0.95rem;
  line-height: 1.4;
  color: rgba(255, 255, 255, 0.95);
}

.cta {
  margin-top: 60px;
  text-align: center;
}

.cta-button {
  background: linear-gradient(to right, #6366f1, #8b5cf6);
  border: none;
  padding: 14px 32px;
  border-radius: 12px;
  font-size: 1rem;
  color: white;
  cursor: pointer;
  font-weight: 600;
  transition: background 0.3s ease;
}

.cta-button:hover {
  background: linear-gradient(to right, #7c3aed, #6d28d9);
}
</style>
