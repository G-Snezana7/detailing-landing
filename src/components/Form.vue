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

// Добавляем аргумент force. По умолчанию он false.
const handleClose = (force = false) => {
  // Не закрываем по клику на крестик/фон, пока идет отправка. 
  // Но если force === true (после успеха), то закрываем в любом случае!
  if (isSending.value && !force) return

  name.value = ''
  phone.value = ''
  emit('close')
}

const handleSubmit = async () => {
  if (!name.value || !phone.value) return

  // Валидация номера телефона (минимум 9 цифр)
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

  // ИСПРАВЛЕНО: Объявляем адрес, который был потерян
  const finalUrl = 'https://web3forms.com'

  try {
    const response = await fetch(finalUrl, {
      method: 'POST',
      body: formData
    })

    const result = await response.json()

    if (result.success) {
      // ИСПРАВЛЕНО: Передаем true, чтобы принудительно закрыть окно
      handleClose(true)

      alert('Thank you! Your request has been successfully sent.')
    } else {
      alert(`Server error: ${result.message || 'Something went wrong'}`)
    }
  } catch (error) {
    console.error('Ошибка при отправке:', error)
    alert('An error occurred. Please check your network connection.')
  } finally {
    isSending.value = false
  }
}
</script>

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
