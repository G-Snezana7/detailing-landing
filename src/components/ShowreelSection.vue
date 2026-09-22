<template>
  <!-- Секция видео-баннера (Блок showreel) -->
  <section class="showreel" aria-label="Video presentation">
    <div class="showreel__container container">
      <div class="showreel__body">

        <!-- Адаптивное фоновое изображение (Retina ready) с относительными путями для Vite -->
        <picture class="showreel__picture">
          <source srcset="
              ../assets/images/showreel-bg.webp    1x,
              ../assets/images/showreel-bg@2x.webp 2x
            " type="image/webp" />
          <source srcset="
              ../assets/images/showreel-bg.png    1x,
              ../assets/images/showreel-bg@2x.png 2x
            " />
          <img src="../assets/images/showreel-bg.png" alt="Detailing Center Showreel Preview" class="showreel__img"
            loading="lazy" decoding="async" />
        </picture>

        <!-- Интерактивная кнопка Play (Элемент управления) -->
        <button class="showreel__play play-btn" type="button" aria-label="Play video" @click="handlePlay">
          <svg class="play-btn__icon" width="48" height="48" viewBox="0 0 48 48" fill="none"
            xmlns="http://www.w3.org/2000/svg" aria-hidden="true">
            <g clip-path="url(#clip0_2_225)">
              <path
                d="M10.2107 1.05836C5.88319 -1.42394 2.37476 0.609593 2.37476 5.59675V42.3997C2.37476 47.3919 5.88319 49.4228 10.2107 46.9428L42.3783 28.4949C46.7073 26.0117 46.7073 21.9886 42.3783 19.506L10.2107 1.05836Z"
                fill="currentColor" />
            </g>
            <defs>
              <clipPath id="clip0_2_225">
                <rect width="48" height="48" fill="currentColor" />
              </clipPath>
            </defs>
          </svg>

          <span class="play-btn__text">Play showreel</span>
        </button>
      </div>
    </div>
  </section>
</template>

<script setup>
// Функция-заглушка для будущего открытия видеоплеера/модалки
const handlePlay = () => {
  console.log('Start playback of the showreel')
}
</script>

<style lang="scss" scoped>
@use '../assets/styles/variables' as *;

.showreel {
  width: 100%;
  // Резиновые отступы: минимум 3.75rem (60px), максимум 6.25rem (100px)
  padding-top: clamp(3.75rem, 6vw, 6.25rem);
  padding-bottom: clamp(3.75rem, 6vw, 5.25rem);

  &__body {
    position: relative;
    width: 100%;
    // Высота баннера плавно сжимается от 600px до 320px на маленьких экранах
    height: clamp(20rem, 45vw, 37.5rem);
    border-radius: 0.75rem;
    /* 12px */
    overflow: hidden;
    display: flex;
    align-items: center;
    justify-content: center;
    background-color: #111;
    /* Временный фон пока грузится картинка */

    /* Затемняющий оверлей поверх картинки */
    &::after {
      content: '';
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background: rgba(0, 0, 0, 0.35);

      z-index: 2;
    }
  }

  &__picture,
  &__img {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    object-fit: cover;
    z-index: 1;
  }
}

/* --- Компонент кнопки Play внутри стилей --- */

.play-btn {
  position: relative;
  z-index: 3;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  background: transparent;
  border: none;
  cursor: pointer;
  color: $color-primary;
  padding: 0;

  // 1. Задаем базовое состояние трансформации
  transform: scale(1);
  // 2. Включаем аппаратное ускорение (will-change) и мягкий cubic-bezier
  will-change: transform;
  transition: transform 0.4s cubic-bezier(0.25, 1, 0.5, 1);

  &__icon {
    width: clamp(2.25rem, 4vw, 3rem);
    height: clamp(2.25rem, 4vw, 3rem);
    margin-bottom: clamp(1rem, 2vw, 1.5rem);

    //Задаем базовое состояние для иконки
    transform: scale(1);
    will-change: transform;
    transition: transform 0.4s cubic-bezier(0.25, 1, 0.5, 1);
  }

  &__text {
    font-family: $font-body;
    font-size: clamp(1rem, 1.5vw, 1.25rem);
    font-weight: 500;
    line-height: 1.2;
    white-space: nowrap;
  }

  &:hover {
    // Увеличиваем кнопку плавно
    transform: scale(1.08);

    .play-btn__icon {
      transform: scale(1.02);
    }
  }

  &:focus-visible {
    outline: 2px solid $color-primary;
    outline-offset: 8px;
    border-radius: 4px;
  }
}
</style>
