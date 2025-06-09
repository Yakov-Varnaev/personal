<template>
  <section class="reviews-section">
    <h2 class="section-title">Отзывы моих менти</h2>
    <div class="reviews-container">
      <v-row
        class="reviews-row"
        align="stretch"
        justify="center"
        dense
        :gap="24"
      >
        <v-col
          v-for="(review, index) in reviews"
          :key="index"
          cols="12"
          sm="6"
          md="4"
          lg="3"
        >
          <div class="review-card stack-style">
            <v-avatar size="72" class="review-avatar mb-4">
              <v-img :src="review.photo" alt="Фото менти" />
            </v-avatar>
            <div class="review-name">{{ review.name }}</div>
            <div class="review-position">{{ review.position }}</div>
            <div class="review-text">{{ review.text }}</div>
          </div>
        </v-col>
      </v-row>
    </div>
  </section>
</template>

<script setup>
const reviews = [
  {
    name: "Анна Смирнова",
    position: "Junior Backend Developer",
    photo: "https://github.com/alohe/memojis/blob/main/png/7924.png?raw=true",
    text: "Работа с Яковом помогла мне быстро разобраться в архитектуре микросервисов и начать уверенно разрабатывать сложные backend-системы.",
  },
  {
    name: "Иван Петров",
    position: "Frontend Engineer",
    photo: "https://github.com/alohe/memojis/blob/main/png/8603.png?raw=true",
    text: "Яков — отличный наставник! Его советы по организации кода и практические рекомендации сильно улучшили мои навыки.",
  },
  {
    name: "Мария Кузнецова",
    position: "DevOps Specialist",
    photo: "https://github.com/alohe/memojis/blob/main/png/6367.png?raw=true",
    text: "Благодаря поддержке Якова я успешно внедрила CI/CD процессы и получила уверенность в работе с Kubernetes и Docker.",
  },
];
</script>

<style scoped>
.reviews-section {
  padding: 64px 24px;
  background: linear-gradient(to bottom, #39597a 0%, #2c5364 50%, #39597a 100%);
  text-align: center;
  color: white;
}

.section-title {
  font-weight: 700;
  font-size: 2.4rem;
  margin-bottom: 48px;
  color: #cce4f7;
}

.reviews-container {
  max-width: 1200px;
  margin: 0 auto;
}

.review-card {
  background: linear-gradient(
    to bottom right,
    rgba(255, 255, 255, 0.15),
    rgba(255, 255, 255, 0.1)
  );
  backdrop-filter: blur(8px);
  border-radius: 20px;
  padding: 24px 20px;
  box-shadow: 0 8px 20px rgba(0, 0, 0, 0.25);
  display: flex;
  flex-direction: column;
  align-items: center;
  transition: transform 0.3s ease;
  min-height: 320px;
  text-align: center;
  user-select: none;
  color: #e0e8f7;
}

.review-card:hover {
  transform: translateY(-8px);
  box-shadow: 0 12px 30px rgba(0, 0, 0, 0.4);
}

.review-avatar {
  border: 3px solid #cce4f7;
  box-sizing: content-box;
  border-radius: 50%;
}

.review-name {
  font-weight: 700;
  font-size: 1.3rem;
  margin-bottom: 6px;
  color: #cce4f7;
}

.review-position {
  font-size: 1rem;
  font-style: italic;
  color: #a3bdd9;
  margin-bottom: 18px;
}

.review-text {
  font-size: 1rem;
  line-height: 1.5;
  color: #d0d9e7;
}
</style>
