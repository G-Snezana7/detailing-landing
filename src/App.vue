<template>
  <div class="app-layout">
    <!-- Добавляем слушатель события от шапки -->
    <AppHeader @open-form="openModal" />

    <main class="app-main">
      <!-- Добавляем слушатели событий от главных секций -->
      <HeroSection @open-form="openModal" />
      <LoveInDetail />
      <ShowreelSection />
      <FeaturesSection />
      <CtaSection @open-form="openModal" />
    </main>

    <AppFooter />

    <Form :is-open="isModalVisible" @close="closeModal" />
  </div>
</template>

<script setup>
import { ref } from 'vue'

import AppHeader from './components/AppHeader.vue'
import HeroSection from './components/HeroSection.vue'
import LoveInDetail from './components/LoveInDetail.vue'
import ShowreelSection from './components/ShowreelSection.vue'
import FeaturesSection from './components/FeaturesSection.vue'
import CtaSection from './components/CtaSection.vue'
import AppFooter from './components/AppFooter.vue'
import Form from './components/Form.vue'

// СОСТОЯНИЕ: создаем переменную, которая управляет показом модалки
const isModalVisible = ref(false)

// ФУНКЦИИ: переключают  переменную
const openModal = () => {
  isModalVisible.value = true
}

const closeModal = () => {
  isModalVisible.value = false
}
</script>

<style lang="scss" scoped>
.app-layout {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
}

.app-main {
  flex-grow: 1;
  /* Чтобы футер всегда прижимался к низу, если контента мало */
}
</style>
