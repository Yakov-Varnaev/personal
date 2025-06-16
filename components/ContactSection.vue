<template>
  <section class="contact-section" id="contact">
    <div class="contact-content">
      <h2 class="section-title">Связаться со мной</h2>
      <form @submit.prevent="submitForm" class="contact-form">
        <label>
          Ваш Email
          <input
            v-model="email"
            type="email"
            required
            placeholder="example@mail.com"
          />
        </label>

        <label>
          Сообщение
          <textarea
            v-model="message"
            rows="5"
            required
            placeholder="Напишите ваше сообщение"
          ></textarea>
        </label>

        <button type="submit">Отправить</button>
      </form>
      <div class="contacts-info">
        <p class="telegram">
          <a href="mailto:yakovvarnaev@yandex.ru">yakovvarnaev@yandex.ru</a>
        </p>
        <p class="telegram">
          <a
            href="https://t.me/YakovVarnaev"
            target="_blank"
            rel="noopener noreferrer"
          >
            <img
              src="/telegram.svg"
              alt="Telegram Icon"
              class="telegram-icon"
            />
            YakovVarnaev
          </a>
        </p>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref } from "vue";

const email = ref("");
const message = ref("");

function submitForm() {
  alert(`Email: ${email.value}\nMessage: ${message.value}`);
  email.value = "";
  message.value = "";
}
</script>

<style scoped>
.contact-section {
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 80px 24px;
  backdrop-filter: blur(20px);
  color: white;
}

.contact-content {
  max-width: 520px;
  width: 100%;
  background: rgba(255, 255, 255, 0.08);
  backdrop-filter: blur(16px);
  border-radius: 20px;
  padding: 40px 32px;
  box-shadow: 0 8px 24px rgba(0, 0, 0, 0.2);
  text-align: center;
  transition: all 0.4s ease;
}

.section-title {
  font-weight: 700;
  font-size: 2rem;
  margin-bottom: 32px;
  color: rgba(255, 255, 255, 0.95);
}

.contact-form label {
  display: block;
  margin-bottom: 20px;
  font-weight: 600;
  color: rgba(255, 255, 255, 0.85);
  text-align: left;
  font-size: 1rem;
}

.contact-form input,
.contact-form textarea {
  width: 100%;
  padding: 12px 16px;
  border-radius: 14px;
  border: none;
  font-size: 1rem;
  background: rgba(255, 255, 255, 0.06);
  color: rgba(255, 255, 255, 0.95);
  backdrop-filter: blur(12px);
  transition: all 0.3s ease;
  margin-top: 8px;
}

.contact-form input::placeholder,
.contact-form textarea::placeholder {
  color: rgba(255, 255, 255, 0.5);
}

.contact-form input:focus,
.contact-form textarea:focus {
  outline: none;
  border: 1px solid #8b5cf6;
  background: rgba(255, 255, 255, 0.1);
}

.contact-form button {
  margin-top: 28px;
  width: 100%;
  padding: 14px 0;
  background: linear-gradient(to right, #6366f1, #8b5cf6);
  color: white;
  border: none;
  border-radius: 14px;
  font-weight: 700;
  font-size: 1.1rem;
  cursor: pointer;
  transition: background 0.3s ease;
}

.contact-form button:hover {
  background: linear-gradient(to right, #7c3aed, #6d28d9);
}

.contacts-info {
  margin-top: 36px;
  font-size: 1rem;
  color: rgba(255, 255, 255, 0.8);
}

.contacts-info a {
  color: #a78bfa;
  text-decoration: none;
  transition: color 0.3s ease;
}

.contacts-info a:hover {
  text-decoration: underline;
}

.telegram {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 10px;
  margin-top: 16px;
}

.telegram a {
  display: inline-flex;
  align-items: center;
  gap: 6px;
  font-weight: 500;
}

.telegram-icon {
  width: 20px;
  height: 20px;
}

/* Dark mode override */
:deep(.v-theme--dark) .contact-content {
  background: rgba(30, 30, 30, 0.85);
  color: rgba(255, 255, 255, 0.95);
  box-shadow: 0 8px 24px rgba(0, 0, 0, 0.6);
}

:deep(.v-theme--dark) .contact-form input,
:deep(.v-theme--dark) .contact-form textarea {
  background: rgba(255, 255, 255, 0.06);
  color: #eee;
}

:deep(.v-theme--dark) .contact-form input:focus,
:deep(.v-theme--dark) .contact-form textarea:focus {
  border-color: #a78bfa;
  background: rgba(255, 255, 255, 0.1);
}

:deep(.v-theme--dark) .contact-form button {
  background: linear-gradient(to right, #8b5cf6, #a78bfa);
  color: #222;
}

:deep(.v-theme--dark) .contact-form button:hover {
  background: linear-gradient(to right, #7c3aed, #6d28d9);
}
</style>
