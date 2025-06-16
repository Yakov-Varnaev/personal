<template>
  <section class="review-section">
    <h2 class="title">Отзывы моих менти</h2>
    <div class="review-container" ref="containerRef">
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
while (reviews.value.length < 5) {
  reviews.value.push({
    ...reviews.value[reviews.value.length % 3],
    text:
      reviews.value[reviews.value.length % 3].text +
      " Дополнительный текст для теста длинных отзывов.",
  });
}

const containerRef = ref(null);
const nodePositions = ref([]);
const nodeVelocities = ref([]);
const draggingIndex = ref(null);
const dragOffset = ref({ x: 0, y: 0 });
const expandedIndex = ref(null);
const focusedIndex = ref(null);

const reviewNodeWidth = 260;
const reviewNodeHeight = 320;
const expandedWidth = 400;
const expandedHeight = 500;

const handleClick = (index) => {
  if (expandedIndex.value === index) return; // не мешаем раскрытой карточке
  focusedIndex.value = index;
};

const toggleExpand = (index) => {
  expandedIndex.value = expandedIndex.value === index ? null : index;
};

// Проверка коллизий
function checkCollisions() {
  for (let i = 0; i < nodePositions.value.length; i++) {
    for (let j = i + 1; j < nodePositions.value.length; j++) {
      const a = nodePositions.value[i];
      const b = nodePositions.value[j];

      const dx = parseFloat(b.left) - parseFloat(a.left);
      const dy = parseFloat(b.top) - parseFloat(a.top);
      const dist = Math.sqrt(dx * dx + dy * dy);

      const radiusA = reviewNodeWidth / 2;
      const radiusB = reviewNodeWidth / 2;
      const minDist = radiusA + radiusB;

      if (dist < minDist) {
        // Простое разделение объектов
        const overlap = (minDist - dist) / 2;
        const nx = dx / dist;
        const ny = dy / dist;

        nodePositions.value[i].left = `${parseFloat(a.left) - nx * overlap}px`;
        nodePositions.value[i].top = `${parseFloat(a.top) - ny * overlap}px`;
        nodePositions.value[j].left = `${parseFloat(b.left) + nx * overlap}px`;
        nodePositions.value[j].top = `${parseFloat(b.top) + ny * overlap}px`;

        // Можно добавить "отскок" — изменить скорость
        nodeVelocities.value[i].x = -nodeVelocities.value[i].x;
        nodeVelocities.value[i].y = -nodeVelocities.value[i].y;
        nodeVelocities.value[j].x = -nodeVelocities.value[j].x;
        nodeVelocities.value[j].y = -nodeVelocities.value[j].y;
      }
    }
  }
}

const startDrag = (index, event) => {
  if (expandedIndex.value === index) return;

  draggingIndex.value = index;

  const nodeRect = event.currentTarget.getBoundingClientRect();

  dragOffset.value.x = event.clientX - nodeRect.left;
  dragOffset.value.y = event.clientY - nodeRect.top;
};

const onMouseMove = (event) => {
  if (draggingIndex.value === null) return;

  const containerRect = containerRef.value.getBoundingClientRect();

  let newLeft = event.clientX - containerRect.left - dragOffset.value.x;
  let newTop = event.clientY - containerRect.top - dragOffset.value.y;

  // Ограничиваем по контейнеру с учётом размеров карточки
  const nodeW =
    expandedIndex.value === draggingIndex.value
      ? expandedWidth
      : reviewNodeWidth;
  const nodeH =
    expandedIndex.value === draggingIndex.value
      ? expandedHeight
      : reviewNodeHeight;

  newLeft = Math.min(Math.max(0, newLeft), containerRect.width - nodeW);
  newTop = Math.min(Math.max(0, newTop), containerRect.height - nodeH);

  nodePositions.value[draggingIndex.value] = {
    left: `${newLeft}px`,
    top: `${newTop}px`,
  };
};

const onMouseUp = () => {
  draggingIndex.value = null;
};

onMounted(() => {
  const containerRect = containerRef.value.getBoundingClientRect();

  nodePositions.value = reviews.value.map(() => ({
    top: `${Math.random() * (containerRect.height - reviewNodeHeight)}px`,
    left: `${Math.random() * (containerRect.width - reviewNodeWidth)}px`,
  }));

  nodeVelocities.value = reviews.value.map(() => ({
    x: (Math.random() - 0.5) * 1.5,
    y: (Math.random() - 0.5) * 1.5,
  }));

  window.addEventListener("mousemove", onMouseMove);
  window.addEventListener("mouseup", onMouseUp);

  const animate = () => {
    const containerRect = containerRef.value.getBoundingClientRect();

    for (let i = 0; i < nodePositions.value.length; i++) {
      if (expandedIndex.value === i || draggingIndex.value == i) continue; // Не двигаем раскрытую

      let left =
        parseFloat(nodePositions.value[i].left) + nodeVelocities.value[i].x;
      let top =
        parseFloat(nodePositions.value[i].top) + nodeVelocities.value[i].y;

      // Проверка границ контейнера
      const nodeW = reviewNodeWidth;
      const nodeH = reviewNodeHeight;

      if (left < 0) {
        left = 0;
        nodeVelocities.value[i].x = -nodeVelocities.value[i].x;
      } else if (left > containerRect.width - nodeW) {
        left = containerRect.width - nodeW;
        nodeVelocities.value[i].x = -nodeVelocities.value[i].x;
      }

      if (top < 0) {
        top = 0;
        nodeVelocities.value[i].y = -nodeVelocities.value[i].y;
      } else if (top > containerRect.height - nodeH) {
        top = containerRect.height - nodeH;
        nodeVelocities.value[i].y = -nodeVelocities.value[i].y;
      }

      nodePositions.value[i].left = `${left}px`;
      nodePositions.value[i].top = `${top}px`;
    }

    checkCollisions();

    requestAnimationFrame(animate);
  };

  animate();
});

const getNodeStyle = (index) => {
  if (expandedIndex.value === index) {
    return {
      top: "50%",
      left: "50%",
      transform: "translate(-50%, -50%) scale(1.05)",
      width: `${expandedWidth}px`,
      maxHeight: `${expandedHeight}px`,
      zIndex: 999,
    };
  }

  if (focusedIndex.value === index) {
    return {
      top: nodePositions.value[index]?.top,
      left: nodePositions.value[index]?.left,
      width: `${reviewNodeWidth}px`,
      maxHeight: `${reviewNodeHeight}px`,
      zIndex: 998,
    };
  }

  return {
    top: nodePositions.value[index]?.top,
    left: nodePositions.value[index]?.left,
    width: `${reviewNodeWidth}px`,
    maxHeight: `${reviewNodeHeight}px`,
    zIndex: 10 + index,
  };
};
</script>

<style scoped>
.review-section {
  padding: 80px 0;
  min-height: 90vh;
  position: relative;
  overflow: hidden;
}

.title {
  font-size: 2rem;
  font-weight: 700;
  text-align: center;
  margin-bottom: 48px;
  color: white;
}

.review-container {
  position: relative;
  width: 100%;
  height: 80vh;
  user-select: none;
}

.review-node {
  position: absolute;
  padding: 16px;
  background: rgba(255, 255, 255, 0.08);
  backdrop-filter: blur(12px);
  border-radius: 16px;
  color: white;
  cursor: grab;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.2);
  overflow: hidden;

  transition-property: transform;
  transition-duration: 0.4s;
  transition-timing-function: ease;
  max-height: 320px;
}

.review-node.expanded {
  cursor: default;
  overflow: auto;
  max-height: 500px;
  width: 400px !important; /* override */
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
