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
        <p>
          Email:
          <a href="mailto:your.email@example.com">your.email@example.com</a>
        </p>
        <p class="telegram">
          <a
            href="https://t.me/yourtelegram"
            target="_blank"
            rel="noopener noreferrer"
          >
            <img
              src="/telegram.svg"
              alt="Telegram Icon"
              class="telegram-icon"
            />
            @yourtelegram
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
  padding: 48px 24px;
  background: linear-gradient(to bottom, #39597a 0%, #2c5364 100%);
}

.contact-content {
  max-width: 480px;
  width: 100%;
  background: rgba(255 255 255 / 0.85);
  backdrop-filter: blur(6px);
  border-radius: 16px;
  padding: 32px 32px 40px;
  box-shadow: 0 8px 24px rgba(0, 0, 0, 0.08);
  text-align: center;
}

.section-title {
  font-weight: 700;
  font-size: 2rem;
  margin-bottom: 32px;
  color: #222;
}

.contact-form label {
  display: block;
  margin-bottom: 16px;
  font-weight: 600;
  color: #333;
  text-align: left;
}

.contact-form input,
.contact-form textarea {
  width: 100%;
  padding: 12px 16px;
  border-radius: 12px;
  border: 1px solid #ddd;
  font-size: 1rem;
  transition: border-color 0.3s ease;
  resize: vertical;
  margin-top: 6px;
}

.contact-form input:focus,
.contact-form textarea:focus {
  outline: none;
  border-color: #4f46e5;
}

.contact-form button {
  margin-top: 28px;
  width: 100%;
  padding: 14px 0;
  background-color: #4f46e5;
  color: white;
  border: none;
  border-radius: 12px;
  font-weight: 700;
  font-size: 1.15rem;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.contact-form button:hover {
  background-color: #4338ca;
}

.contacts-info {
  margin-top: 28px;
  font-size: 1rem;
  color: #444;
}

.contacts-info a {
  color: #4f46e5;
  text-decoration: none;
}

.contacts-info a:hover {
  text-decoration: underline;
}

.telegram {
  display: flex;
  align-items: center;
  gap: 8px;
  margin-top: 12px;
}

.telegram a {
  display: inline-flex;
  align-items: center;
  gap: 6px;
  color: #4f46e5;
  text-decoration: none;
  font-weight: 500;
}

.telegram a:hover {
  text-decoration: underline;
}

.telegram-icon {
  width: 20px;
  height: 20px;
  display: inline-block;
}

.telegram-link {
  display: inline-flex;
  align-items: center;
  color: #4f46e5;
  text-decoration: none;
}

.telegram-link:hover {
  text-decoration: underline;
}

/* Dark theme support */
:deep(.v-theme--dark) .contact-content {
  background: rgba(30 30 30 / 0.85);
  color: #eee;
  box-shadow: 0 8px 24px rgba(0, 0, 0, 0.6);
}

:deep(.v-theme--dark) .contact-form label {
  color: #ddd;
}

:deep(.v-theme--dark) .contact-form input,
:deep(.v-theme--dark) .contact-form textarea {
  background: #222;
  border: 1px solid #444;
  color: #eee;
}

:deep(.v-theme--dark) .contact-form input:focus,
:deep(.v-theme--dark) .contact-form textarea:focus {
  border-color: #a78bfa;
}

:deep(.v-theme--dark) .contact-form button {
  background-color: #a78bfa;
  color: #222;
}

:deep(.v-theme--dark) .contact-form button:hover {
  background-color: #7c3aed;
}

:deep(.v-theme--dark) .contacts-info {
  color: #ccc;
}

:deep(.v-theme--dark) .contacts-info a {
  color: #a78bfa;
}
</style>
