<template>
  <section class="review-section">
    <div class="review-container">
      <div
        v-for="(review, index) in reviews"
        :key="index"
        class="review-node"
        :style="getNodeStyle(index)"
        :class="{ expanded: expandedIndex === index }"
        @mousedown="startDrag(index, $event)"
        @click="handleClick(index)"
      >
        <img :src="review.photo" class="avatar" />
        <div class="review-info">
          <h3>{{ review.name }}</h3>
          <p class="position">{{ review.position }}</p>
          <p class="text" :class="{ truncate: expandedIndex !== index }">
            {{ review.text }}
          </p>
          <button class="expand-btn" @click.stop="toggleExpand(index)">
            {{ expandedIndex === index ? "Свернуть" : "Развернуть" }}
          </button>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref, onMounted } from "vue";

const focusedIndex = ref(null);

const handleClick = (index) => {
  if (expandedIndex.value === index) return; // не мешаем раскрытой карточке
  focusedIndex.value = index;
};

const reviews = ref([
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
]);

// Дополняем до 10
while (reviews.value.length < 10) {
  reviews.value.push({
    ...reviews.value[reviews.value.length % 3],
    text:
      reviews.value[reviews.value.length % 3].text +
      " Дополнительный текст для теста длинных отзывов.",
  });
}

const nodePositions = ref([]);
const draggingIndex = ref(null);
const expandedIndex = ref(null);

const startDrag = (index, event) => {
  // Блокируем перетаскивание развернутой карточки
  if (expandedIndex.value === index) return;

  draggingIndex.value = index;
  const startX = event.clientX;
  const startY = event.clientY;
  const node = nodePositions.value[index];

  const onMouseMove = (e) => {
    const dx = e.clientX - startX;
    const dy = e.clientY - startY;
    nodePositions.value[index] = {
      top: `${parseInt(node.top) + dy}px`,
      left: `${parseInt(node.left) + dx}px`,
    };
  };

  const onMouseUp = () => {
    draggingIndex.value = null;
    document.removeEventListener("mousemove", onMouseMove);
    document.removeEventListener("mouseup", onMouseUp);
  };

  document.addEventListener("mousemove", onMouseMove);
  document.addEventListener("mouseup", onMouseUp);
};

const toggleExpand = (index) => {
  expandedIndex.value = expandedIndex.value === index ? null : index;
};

onMounted(() => {
  nodePositions.value = reviews.value.map(() => ({
    top: `${Math.random() * 500 + 50}px`,
    left: `${Math.random() * 500 + 50}px`,
  }));
});

const getNodeStyle = (index) => {
  if (expandedIndex.value === index) {
    return {
      top: "50%",
      left: "50%",
      transform: "translate(-50%, -50%) scale(1.05)",
      zIndex: 999,
    };
  }

  if (focusedIndex.value === index) {
    return {
      top: nodePositions.value[index]?.top,
      left: nodePositions.value[index]?.left,
      zIndex: 998,
    };
  }

  return {
    top: nodePositions.value[index]?.top,
    left: nodePositions.value[index]?.left,
    zIndex: 10 + index,
  };
};
</script>

<style scoped>
.review-section {
  min-height: 100vh;
  background: linear-gradient(to bottom, #1f2937, #2c3e50);
  position: relative;
  overflow: hidden;
}

.review-container {
  position: relative;
  width: 100%;
  height: 100vh;
}

.review-node {
  position: absolute;
  width: 260px;
  padding: 16px;
  background: rgba(255, 255, 255, 0.08);
  backdrop-filter: blur(12px);
  border-radius: 16px;
  color: white;
  cursor: grab;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.2);
  transition: all 0.4s ease;
  max-height: 320px;
  overflow: hidden;

  transition-property: transform;
  transition-duration: 0.4s;
  transition-timing-function: ease;
}

.review-node.expanded {
  width: 400px;
  max-height: 500px;
  cursor: default;
  overflow: auto;
}

.avatar {
  width: 48px;
  height: 48px;
  border-radius: 50%;
  object-fit: cover;
  margin-bottom: 12px;
}

.review-info h3 {
  margin: 0;
  font-size: 1rem;
  font-weight: bold;
}

.review-info .position {
  font-size: 0.9rem;
  color: #a0aec0;
  margin-bottom: 8px;
}

.review-info .text {
  font-size: 0.85rem;
  line-height: 1.4;
  max-height: 5.2em;
  overflow: hidden;
  text-overflow: ellipsis;
  transition: max-height 0.3s ease;
}

.review-node.expanded .text {
  max-height: none;
}

.expand-btn {
  margin-top: 12px;
  background: rgba(255, 255, 255, 0.12);
  border: none;
  padding: 6px 12px;
  color: white;
  border-radius: 8px;
  cursor: pointer;
  font-size: 0.8rem;
  transition: background 0.2s ease;
}

.expand-btn:hover {
  background: rgba(255, 255, 255, 0.22);
}
</style>
