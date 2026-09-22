<template>
  <header class="header">
    <div class="header__container container">
      <!-- Логотип -->
      <a href="#" class="header__logo" aria-label="LuxuryDetails Home page">
        LuxuryDetails
      </a>

      <!-- Бургер-кнопка (только для планшетов и мобильных) -->
      <button class="header__burger" :class="{ 'header__burger--active': isMenuOpen }" @click="toggleMenu"
        :aria-expanded="isMenuOpen" aria-label="Open mobile menu">
        <span></span>
        <span></span>
        <span></span>
      </button>

      <!-- Навигационное меню -->
      <nav class="header__nav" :class="{ 'header__nav--open': isMenuOpen }" aria-label="Главная навигация">
        <ul class="header__menu">
          <li v-for="item in menuItems" :key="item.id" class="header__item">
            <a :href="item.href" class="header__link" @click="closeMenu">
              {{ item.label }}
            </a>
          </li>
        </ul>

        <!-- Мобильная кнопка действия (вешаем клик + закрываем мобильное меню) -->
        <a href="#contact" class="header__btn header__btn--mobile" @click.prevent="openFormModal">
          Get a quote
        </a>
      </nav>

      <!-- Десктопная кнопка действия (вешаем клик) -->
      <a href="#contact" class="header__btn header__btn--desktop" @click.prevent="openFormModal">
        Get a quote
      </a>
    </div>
  </header>
</template>

<script setup>
import { ref } from 'vue'

// 1. Объявляем событие, которое полетит в App.vue
const emit = defineEmits(['open-form'])

const menuItems = [
  { id: 'services', label: 'Services', href: '#services' },
  { id: 'pricing', label: 'Pricing', href: '#pricing' },
  { id: 'about', label: 'About', href: '#about' },
  { id: 'contact', label: 'Contact', href: '#contact' },
]

const isMenuOpen = ref(false)

const toggleMenu = () => {
  isMenuOpen.value = !isMenuOpen.value
}

const closeMenu = () => {
  isMenuOpen.value = false
}

// 2. Функция, которая закрывает бургер (если он был открыт) и триггерит модалку
const openFormModal = () => {
  closeMenu()
  emit('open-form')
}
</script>


<style lang="scss" scoped>
@use '../assets/styles/variables' as *;

.header {
  padding-top: 1.5rem;
  font-family: $font-title;
  position: relative;
  z-index: 100;

  &__container {
    display: flex;
    justify-content: space-between;
    align-items: center;
    width: 100%;
  }

  &__logo {
    font-size: 1.25rem;
    font-weight: 500;
    line-height: 1.5;
    color: $color-primary;
    position: relative;
    z-index: 101;
  }

  &__burger {
    display: none;
    flex-direction: column;
    justify-content: space-between;
    width: 30px;
    height: 20px;
    background: transparent;
    border: none;
    cursor: pointer;
    padding: 0;
    position: relative;
    z-index: 101;

    span {
      display: block;
      width: 100%;
      height: 2px;
      background-color: $color-primary;
      transition: transform 0.3s ease, opacity 0.3s ease;
    }

    &--active {
      span:nth-child(1) {
        transform: translateY(9px) rotate(45deg);
      }

      span:nth-child(2) {
        opacity: 0;
      }

      span:nth-child(3) {
        transform: translateY(-9px) rotate(-45deg);
      }
    }

    @include tablet {
      display: flex;
    }
  }

  &__nav {
    @include tablet {
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100vh;
      background-color: $color-bg;
      padding: 8rem 2rem 2rem;
      transform: translateX(100%);
      transition: transform 0.4s ease;
      display: flex;
      flex-direction: column;
      align-items: center;

      &--open {
        transform: translateX(0);
      }
    }
  }

  &__menu {
    display: flex;
    gap: 2rem;

    @include tablet {
      flex-direction: column;
      align-items: center;
      gap: 2.5rem;
    }
  }

  &__link {
    font-size: 1rem;
    font-weight: 400;
    line-height: 1.5;
    color: $color-primary;
    transition: color 0.3s ease;

    &:hover {
      color: $color-text-muted;
    }

    &:focus-visible {
      outline: 2px solid $color-primary;
      outline-offset: 4px;
    }

    @include tablet {
      font-size: 1.5rem;
    }
  }

  &__btn {
    font-size: 1rem;
    font-weight: 500;
    line-height: 1.5;
    color: $color-primary;
    padding: 1.156rem 1.625rem;
    border: 1px solid $color-primary;
    border-radius: 10px;
    background: transparent;
    text-align: center;
    transition: background-color 0.3s ease, color 0.3s ease;

    &:hover {
      background-color: $color-primary;
      color: $color-bg;
    }

    &:focus-visible {
      outline: 2px solid $color-primary;
      outline-offset: 4px;
    }

    // Логика отображения десктопной кнопки
    &--desktop {
      @include tablet {
        display: none;
      }
    }

    // Логика отображения мобильной кнопки
    &--mobile {
      display: none;

      @include tablet {
        display: inline-block;
        margin-top: 3rem;
        width: 100%;
        max-width: 280px;
      }
    }
  }
}
</style>
