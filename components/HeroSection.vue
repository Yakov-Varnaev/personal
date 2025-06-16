<template>
  <section class="hero-section" id="hero">
    <v-container class="hero-inner">
      <!-- Левая часть: текст -->
      <div class="hero-text">
        <h1 class="hero-title">Привет, я Яков Варнаев</h1>
        <p class="hero-typing">
          <span ref="typedText">{{ typed }}</span>
          <span class="cursor">|</span>
        </p>

        <v-btn
          class="contact-button"
          elevation="0"
          rounded="lg"
          size="large"
          @click="scrollTo('contact')"
        >
          Связаться
        </v-btn>

        <div class="hero-links">
          <p class="hero-subtitle">На этом сайте:</p>
          <div class="hero-nav">
            <button @click="scrollTo('about')">Обо мне</button>
            <button @click="scrollTo('skills')">Навыки</button>
            <button @click="scrollTo('review')">Отзывы</button>
            <button @click="scrollTo('benefits')">
              Зачем тебе менторство?
            </button>
            <button @click="scrollTo('contact')">Контакты</button>
          </div>
        </div>
      </div>

      <!-- Правая часть: фото -->
      <div class="hero-photo">
        <v-img
          src="/yakov.jpeg"
          alt="Фото Якова"
          width="240"
          height="240"
          cover
          class="photo-img"
        />
      </div>
    </v-container>
  </section>
</template>

<script setup>
import { ref, onMounted } from "vue";

const phrases = [
  "Senior Backend Developer",
  "Архитектор микросервисов",
  "Лидер команды в Яндексе",
];
const typed = ref("");
let currentPhrase = 0;
let charIndex = 0;

const typedText = ref(null);

const typeNextChar = () => {
  const phrase = phrases[currentPhrase];
  if (charIndex < phrase.length) {
    typed.value += phrase[charIndex++];
    setTimeout(typeNextChar, 60);
  } else {
    setTimeout(eraseText, 1600);
  }
};

const eraseText = () => {
  if (charIndex > 0) {
    typed.value = typed.value.slice(0, --charIndex);
    setTimeout(eraseText, 30);
  } else {
    currentPhrase = (currentPhrase + 1) % phrases.length;
    setTimeout(typeNextChar, 600);
  }
};

onMounted(() => {
  setTimeout(typeNextChar, 800);
});

const scrollTo = (id) => {
  const el = document.getElementById(id);
  if (el) {
    el.scrollIntoView({ behavior: "smooth" });
  }
};
</script>

<style scoped>
.hero-section {
  height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  /* background: linear-gradient(to bottom, #0f2027 0%, #203a43 50%); */
  padding: 0 16px;
  color: white;
  text-align: left;
  overflow: hidden;
}

.hero-inner {
  display: flex;
  flex-direction: row;
  align-items: center;
  justify-content: space-between;
  max-width: 1100px;
  width: 100%;
  animation: fadeInUp 1.2s ease-out;
}

.hero-text {
  flex: 1;
  padding-right: 32px;
}

.hero-title {
  font-size: 3rem;
  font-weight: 700;
  margin-bottom: 16px;
}

.hero-typing {
  font-size: 1.5rem;
  height: 2rem;
  margin-bottom: 32px;
  font-family: monospace;
  color: #dcdcdc;
}

.cursor {
  display: inline-block;
  width: 1px;
  background: transparent;
  animation: blink 1s step-start infinite;
}

.contact-button {
  background-color: #2563eb;
  color: white;
  font-weight: 600;
  padding: 10px 24px;
  transition:
    background-color 0.3s ease,
    transform 0.2s ease;
  text-transform: none;
  letter-spacing: 0.5px;
}

.contact-button:hover {
  background-color: #1d4ed8; /* немного темнее при ховере */
  transform: translateY(-2px);
}

.contact-button:active {
  transform: scale(0.97);
}

/* Тёмная тема */
:deep(.v-theme--dark) .contact-button {
  background-color: #3b82f6;
  color: white;
}

:deep(.v-theme--dark) .contact-button:hover {
  background-color: #2563eb;
}

@keyframes blink {
  50% {
    opacity: 0;
  }
}

.hero-btn {
  font-weight: 600;
}

.hero-photo {
  flex-shrink: 0;
}

.photo-img {
  border-radius: 50%;
  box-shadow: 0 0 24px rgba(255, 255, 255, 0.1);
}

/* Адаптивность */
@media (max-width: 768px) {
  .hero-inner {
    flex-direction: column;
    text-align: center;
  }

  .hero-text {
    padding: 0;
  }

  .hero-photo {
    margin-top: 24px;
  }
}

/* Темная тема (уже по умолчанию) */
:deep(.v-theme--light) .hero-section {
  background: linear-gradient(to bottom right, #f5f7fa, #c3cfe2);
  color: #222;
}

.hero-links {
  margin-top: 40px;
  text-align: left;
}

.hero-subtitle {
  font-size: 1rem;
  margin-bottom: 12px;
  color: #ccc;
}

.hero-nav {
  display: flex;
  flex-wrap: wrap;
  gap: 12px;
}

.hero-nav button {
  padding: 8px 16px;
  background: rgba(255, 255, 255, 0.08);
  color: white;
  font-size: 0.9rem;
  border: none;
  border-radius: 12px;
  cursor: pointer;
  backdrop-filter: blur(10px);
  transition: background 0.3s ease;
}

.hero-nav button:hover {
  background: rgba(255, 255, 255, 0.18);
}
</style>
