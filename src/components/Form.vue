<script setup>
import { ref } from 'vue'

defineProps({
  isOpen: {
    type: Boolean,
    required: true
  }
})

const emit = defineEmits(['close'])

const name = ref('')
const phone = ref('')
const isSending = ref(false)

// КЛЮЧ WEB3FORMS 
const WEB3FORMS_KEY = import.meta.env.VITE_WEB3FORMS_KEY

const handleClose = () => {
  // Запрещаем закрывать окно, если сейчас идет отправка данных на сервер
  if (isSending.value) return

  name.value = ''
  phone.value = ''
  emit('close')
}

const handleSubmit = async () => {
  if (!name.value || !phone.value) return

  // Коммерческая валидация: проверяем, что введено хотя бы 9 цифр (длина кода + номера в РБ)
  const digitsOnly = phone.value.replace(/\D/g, '')
  if (digitsOnly.length < 9) {
    alert('Please enter a valid phone number!')
    return
  }

  isSending.value = true

  const formData = new FormData()
  formData.append('access_key', WEB3FORMS_KEY)
  formData.append('subject', 'New Request from LuxuryDetails')
  formData.append('name', name.value)
  formData.append('phone', phone.value)



  try {
    const response = await fetch(finalUrl, {
      method: 'POST',
      body: formData
    })

    const result = await response.json()

    if (result.success) {
      alert('Thank you! Your request has been successfully sent.')
      // 1. ОБЯЗАТЕЛЬНО ВЫЗЫВАЕМ ЗАКРЫТИЕ И ОЧИСТКУ ПОЛЕЙ:
      handleClose()
    } else {
      alert(`Server error: ${result.message || 'Something went wrong'}`)
    }
  } catch (error) {
    console.error('Ошибка при отправке:', error)
    alert('An error occurred. Please check your network connection.')
  } finally {
    // 2. ВОЗВРАЩАЕМ КНОПКЕ АКТИВНОЕ СОСТОЯНИЕ (Sending... меняется обратно):
    isSending.value = false
  }

</script>

<template>
  <Transition name="fade">
    <div v-if="isOpen" class="modal-overlay" @click.self="handleClose">
      <!-- Добавляем роль диалогового окна для доступности (A11y) -->
      <div class="modal-content" role="dialog" aria-modal="true">

        <!-- Кнопка закрытия теперь доступна для скринридеров и блокируется при отправке -->
        <button class="modal-close" @click="handleClose" :disabled="isSending" aria-label="Close modal window">
          &times;
        </button>

        <h3 class="modal-title">Request a Details</h3>
        <p class="modal-subtitle">Leave your contact details and we will call you back</p>

        <form @submit.prevent="handleSubmit" class="modal-form">
          <div class="form-group">
            <!-- aria-label заменяет скрытый тег <label> и делает код доступным -->
            <input v-model.trim="name" type="text" placeholder="Your name" required class="form-input"
              aria-label="Full Name" :disabled="isSending" />
          </div>

          <div class="form-group">
            <input v-model.trim="phone" type="tel" placeholder="+375 (__) ___-__-__" required class="form-input"
              aria-label="Phone number" :disabled="isSending" />
          </div>

          <button type="submit" :disabled="isSending" class="form-submit-btn">
            {{ isSending ? 'Sending...' : 'Submit Request' }}
          </button>
        </form>
      </div>
    </div>
  </Transition>
</template>
<style lang="scss" scoped>
.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.8);
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 1000;
}

.modal-content {
  background: #1a1a1a;
  border: 1px solid #333;
  padding: 40px;
  border-radius: 12px;
  position: relative;
  max-width: 450px;
  width: 90%;
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.5);
}

.modal-close {
  position: absolute;
  top: 15px;
  right: 15px;
  background: none;
  border: none;
  color: #888;
  font-size: 28px;
  cursor: pointer;

  &:hover {
    color: #fff;
  }
}

.form-input {
  width: 100%;
  padding: 12px;
  margin-bottom: 20px;
  background: #262626;
  border: 1px solid #444;
  color: #fff;
  border-radius: 6px;

  &:focus {
    border-color: #fff;
    outline: none;
  }
}

.form-submit-btn {
  width: 100%;
  padding: 14px;
  background: #fff;
  color: #000;
  border: none;
  font-weight: bold;
  border-radius: 6px;
  cursor: pointer;
  transition: opacity 0.2s;

  &:disabled {
    opacity: 0.5;
    cursor: not-allowed;
  }
}

/* Классы анимации Vue Transition */

// Эффект плавного появления и исчезновения для всего фона
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.3s ease;

  // Дополнительно анимируем само белое окошко, чтобы оно слегка увеличивалось при появлении
  .modal-content {
    transition: transform 0.3s ease;
  }
}

// Начальное состояние при появлении и конечное при исчезновении
.fade-enter-from,
.fade-leave-to {
  opacity: 0;

  .modal-content {
    transform: scale(0.9); // Окошко плавно увеличивается с 90% до 100%
  }
}
</style>
