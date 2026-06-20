<template>
  <div class="feedback-container">
    <h2 class="feedback-title">Обратная связь</h2>
    <p class="feedback-subtitle">Напишите нам, и мы обязательно ответим</p>

    <form @submit.prevent="handleSubmit" class="feedback-form">
      <div class="form-grid">
        <div class="form-group">
          <label>Имя <span class="required">*</span></label>
          <input
            v-model="form.name"
            type="text"
            placeholder="Ваше имя"
            required
          />
        </div>

        <div class="form-group">
          <label>Телефон</label>
          <input
            v-model="form.phone"
            type="tel"
            placeholder="+7 (___) ___-__-__"
          />
        </div>

        <div class="form-group">
          <label>E-mail <span class="required">*</span></label>
          <input
            v-model="form.email"
            type="email"
            placeholder="your@email.ru"
            required
          />
        </div>

        <div class="form-group">
          <label>Тема</label>
          <input
            v-model="form.subject"
            type="text"
            placeholder="Например: Доставка, Вопрос по ассортименту"
          />
        </div>
      </div>

      <div class="form-group full">
        <label>Ваш вопрос или пожелание <span class="required">*</span></label>
        <textarea
          v-model="form.message"
          rows="6"
          placeholder="Напишите здесь всё, что хотите нам сообщить..."
          required
        ></textarea>
      </div>

      <button type="submit" class="submit-btn" :disabled="isLoading">
        {{ isLoading ? 'Отправляем...' : 'Отправить сообщение' }}
      </button>

      <p class="privacy">Мы ответим в течение 24 часов</p>
    </form>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const form = ref({
  name: '',
  phone: '',
  email: '',
  subject: '',
  message: ''
})

const isLoading = ref(false)

const handleSubmit = async () => {
  if (!form.value.name || !form.value.email || !form.value.message) {
    alert('Пожалуйста, заполните обязательные поля')
    return
  }

  isLoading.value = true

  try {
    // await $fetch('/api/feedback', { method: 'POST', body: form.value })
    
    alert('Спасибо! Ваше сообщение отправлено.')
    
    form.value = { name: '', phone: '', email: '', subject: '', message: '' }
  } catch (e) {
    alert('Ошибка отправки. Попробуйте позже.')
  } finally {
    isLoading.value = false
  }
}
</script>

<style scoped>
.feedback-container {
  max-width: var(--container-3xl);
  border-radius: 16px;
  width: 100%;
  min-height: 800px;
}

.feedback-title {
  text-align: center;
  font-size: var(--text-3xl);
  font-weight: var(--font-weight-normal);
  margin-bottom: 8px;
  color: var(--color-gray-900);
  font-family: var(--font-rubik);
}

.feedback-subtitle {
  text-align: center;
  color: var(--color-gray-600);
  margin-bottom: 32px;
  font-family: var(--font-nunito);
  font-size: var(--text-lg);
}

.feedback-form {
  display: flex;
  flex-direction: column;
  gap: 80px;
}

.form-grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 20px;
}

.form-group.full {
  grid-column: 1 / -1;
}

.form-group label {
  display: block;
  margin-bottom: 8px;
  font-weight: var(--font-weight-semibold);
  color: var(--color-gray-900);
  font-size: var(--text-base);
}

.form-group input,
.form-group textarea {
  width: 100%;
  padding: 14px 16px;
  border: 2px solid var(--color-gray-300);
  border-radius: 10px;
  font-size: var(--text-base);
  transition: all 0.3s;
  background: var(--color-white);
}

.form-group input:focus,
.form-group textarea:focus {
  outline: none;
  border-color: var(--color-orange-600);
  box-shadow: 0 0 0 3px rgba(249, 115, 22, 0.15);
}

.required {
  color: var(--color-red-600);
}

.submit-btn {
  margin-top: 10px;
  padding: 16px 32px;
  background: var(--color-orange-600);
  color: var(--color-white);
  font-size: var(--text-lg);
  font-weight: var(--font-weight-semibold);
  font-family: var(--font-nunito);
  border: none;
  border-radius: 10px;
  cursor: pointer;
  transition: all 0.3s;
}

.submit-btn:hover:not(:disabled) {
  background: var(--color-orange-700);
  transform: translateY(-2px);
}

.submit-btn:disabled {
  opacity: 0.7;
  cursor: not-allowed;
}

.privacy {
  text-align: center;
  font-size: var(--text-sm);
  color: var(--color-gray-600);
  margin-top: 16px;
  font-family: var(--font-nunito);
}

label {
    font-family: var(--font-nunito);
}

/* Адаптив */
@media (max-width: 640px) {
  .form-grid {
    grid-template-columns: 1fr;
  }
  
  .feedback-container {
    padding: 30px 20px;
    margin: 20px auto;
    min-width: 400px;
  }
}
</style>