<template>
  <section class="details" id="services" aria-labelledby="details-title">
    <div class="container">

      <!-- Верхний маркер и разделительная линия -->
      <span class="details__marker">Luxury car detailing</span>
      <div class="details__line" aria-hidden="true"></div>

      <!-- Контентный блок: Заголовок и описание -->
      <div class="details__intro">
        <h2 id="details-title" class="details__title">Love in Every Detail</h2>
        <p class="details__text">
          Immerse yourself in luxury with our bespoke detailing packages tailored to your car's unique needs.
        </p>
      </div>

      <!-- Сетка карточек услуг (Адаптивный CSS Grid) -->
      <div class="details__grid">
        <article v-for="(service, index) in services" :key="index" class="details-card">
          <div class="details-card__image-wrapper">
            <img :src="service.image" :alt="service.title" class="details-card__image" loading="lazy"
              decoding="async" />
          </div>
          <h3 class="details-card__title">{{ service.title }}</h3>
          <p class="details-card__text">{{ service.desc }}</p>

          <a href="#" class="details-card__link">
            <span class="details-card__link-text">
              Learn more
              <!-- Доступность: скрытый текст для скринридеров -->
              <span class="visually-hidden"> about {{ service.title }}</span>
            </span>
            <svg class="details-card__link-icon" width="16" height="11" viewBox="0 0 16 11" fill="none"
              xmlns="http://www.w3.org/2000/svg" aria-hidden="true">
              <path d="M0 5.35355H14.5" stroke="currentColor" />
              <path d="M9.5 0.353546L14.5 5.35355L9.5 10.3535" stroke="currentColor" />
            </svg>
          </a>
        </article>
      </div>

    </div>
  </section>
</template>

<script setup>
import { ref } from 'vue'

// Данные карточек услуг
const services = ref([
  {
    title: 'Entry level detail',
    desc: 'Treat your luxury car to a thorough hand wash and wax application.',
    image: new URL('../assets/images/detail-1.webp', import.meta.url).href
  },
  {
    title: 'Maintenance detail',
    desc: 'Ensure your car\'s longevity with a periodic exterior protection treatment.',
    image: new URL('../assets/images/detail-2.webp', import.meta.url).href
  },
  {
    title: 'Full detail',
    desc: 'Pamper your vehicle with a complete treatment, leaving no detail overlooked.',
    image: new URL('../assets/images/detail-3.webp', import.meta.url).href
  }
])
</script>

<style lang="scss" scoped>
@use '../assets/styles/variables' as *;

.details {
  width: 100%;
  background-color: $color-bg;
  padding-bottom: clamp(3rem, 6vw, 4.9375rem);
  /* Резиновый нижний отступ */

  &__marker {
    display: block;
    font-family: $font-title;
    font-size: clamp(1rem, 1.5vw, 1.25rem);
    /* Плавный шрифт маркера */
    font-weight: 500;
    line-height: 1.2;
    color: $color-text-muted;
    margin-bottom: clamp(1.5rem, 3vw, 2.5rem);
  }

  &__line {
    width: 100%;
    height: 1px;
    background-color: $color-text-muted;
    margin-bottom: clamp(2rem, 4vw, 3rem);
  }

  &__intro {
    display: flex;
    justify-content: space-between;
    align-items: flex-start;
    margin-bottom: clamp(3rem, 6vw, 5rem);

    // Перестраиваем заголовок и текст в один столбец на планшетах/мобилках
    @include tablet {
      flex-direction: column;
      gap: 1.5rem;
    }
  }

  &__title {
    font-family: $font-title;
    font-size: clamp(2rem, 4vw, 3rem);
    /* Резиновый h2 заголовок */
    font-weight: 500;
    line-height: 1.1;
    color: $color-primary;
    max-width: 28.125rem;
    width: 100%;
  }

  &__text {
    font-family: $font-body;
    font-size: clamp(1.125rem, 2vw, 1.5rem);
    /* Резиновый текст описания */
    font-weight: 400;
    line-height: 1.3;
    color: $color-text-muted;
    max-width: 34rem;
    width: 100%;
  }

  &__grid {
    // Адаптивная сетка без медиа-запросов
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
    gap: 2rem;
    /* Расстояние между карточками */
  }
}

.details-card {
  display: flex;
  flex-direction: column;

  &__image-wrapper {
    width: 100%;
    height: clamp(15rem, 25vw, 22rem);
    /* Картинка сжимается на маленьких экранах */
    overflow: hidden;
    border-radius: 8px;
    margin-bottom: 2rem;
  }

  &__image {
    width: 100%;
    height: 100%;
    object-fit: cover;
    display: block;
    transition: transform 0.5s ease;
  }

  &:hover &__image {
    transform: scale(1.04);
  }

  &__title {
    font-family: $font-title;
    font-size: clamp(1.25rem, 2vw, 1.5rem);
    font-weight: 500;
    line-height: 1.2;
    color: $color-primary;
    margin-bottom: 1.25rem;
  }

  &__text {
    font-family: $font-body;
    font-size: 1rem;
    font-weight: 400;
    line-height: 1.5;
    color: $color-text-muted;
    margin-bottom: 2rem;
    flex-grow: 1;
    /* Выталкивает кнопку вниз */
  }

  &__link {
    display: inline-flex;
    align-items: center;
    gap: 1rem;
    color: $color-primary;
    text-decoration: none;
    font-family: $font-body;
    font-size: 1rem;
    font-weight: 400;
    line-height: 1.5;
    width: fit-content;
    transition: color 0.25s ease;

    &:hover {
      color: $color-text-light-grey;

      .details-card__link-icon {
        transform: translateX(5px);
        /* Смещаем стрелочку вправо при ховере */
      }
    }
  }

  &__link-icon {
    transition: transform 0.25s ease;
  }
}
</style>
