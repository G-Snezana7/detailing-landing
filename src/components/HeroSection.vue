<template>
  <section class="hero" aria-label="Home screen">
    <!-- Текстовый контент зажат в контейнер 1120px -->
    <div class="hero__container container">
      <div class="hero__content">
        <h1 class="hero__title">Luxury car detailing</h1>
        <p class="hero__subtitle">
          Experience the prestige of a professionally detailed car,
          radiating elegance and refinement at every turn.
        </p>
        <a href="#contact" class="hero__link-action">
          <span class="hero__link-text">Let's connect</span>
          <svg class="hero__link-icon" width="18" height="18" viewBox="0 0 18 18" fill="none" xmlns="http://w3.org"
            aria-hidden="true">
            <path
              d="M17.707 1C17.707 0.447715 17.2593 0 16.707 0H7.70703C7.15475 0 6.70703 0.447715 6.70703 1C6.70703 1.55228 7.15475 2 7.70703 2H15.707V10C15.707 10.5523 16.1547 11 16.707 11C17.2593 11 17.707 10.5523 17.707 10V1ZM1.41414 17.7071L17.4141 1.70711L15.9999 0.292893L-7.55191e-05 16.2929L1.41414 17.7071Z"
              fill="currentColor" />
          </svg>
        </a>
      </div>
    </div>

    <!-- Блок картинки вынесен за пределы контейнера, чтобы занять всю ширину экрана -->
    <div class="hero__image-wrapper">
      <picture>
        <source srcset="
                ../assets/images/hero-car.webp    1x,
                ../assets/images/hero-car@2x.webp 2x
              " type="image/webp" />
        <source srcset="
                ../assets/images/hero-car.png    1x,
                ../assets/images/hero-car@2x.png 2x
              " />
        <img src="../assets/images/hero-car.png" alt="A premium car in a detailing studio" class="hero__image"
          fetchpriority="high" decoding="async" />
      </picture>
    </div>
  </section>
</template>

<script setup>
// Логика пока не требуется
</script>

<style lang="scss" scoped>
@use '../assets/styles/variables' as *;

.hero {
  width: 100%;
  // Резиновый отступ сверху: минимум 4rem (64px) на мобилке, максимум 7.5rem (120px) на десктопе
  padding-top: clamp(4rem, 6vw, 7.5rem);
  display: flex;
  flex-direction: column;
  align-items: center;
  font-family: $font-title;

  &__content {
    max-width: 57.5rem;
    /* 920px */
    width: 100%;
    margin-left: auto;
    /* Идеальное стандартное центрирование */
    margin-right: auto;
    /* Идеальное стандартное центрирование */
    display: flex;
    flex-direction: column;
    align-items: center;
    text-align: center;
  }


  &__title {

    font-size: clamp(2.5rem, 7vw, 6rem);
    font-weight: 500;
    line-height: 1.1;
    color: $color-primary;
    // Резиновый отступ снизу
    margin-bottom: clamp(1.5rem, 4vw, 3rem);
  }

  &__subtitle {
    font-family: $font-body;
    // Шрифт подзаголовка  слегка уменьшаем на мобильных (от 16px до 20px)
    font-size: clamp(1rem, 1.5vw, 1.25rem);
    font-weight: 400;
    line-height: 1.5;
    color: $color-text-hero-sub;
    max-width: 32.31rem;
    /* 517px */
    margin-bottom: clamp(2rem, 3.5vw, 2.5rem);
  }

  &__link-action {
    display: inline-flex;
    align-items: center;
    background: transparent;
    border: none;
    padding: 0;
    // Отступ до картинки плавно уменьшается на телефонах
    margin-bottom: clamp(3.5rem, 8vw, 6.06rem);
    color: $color-primary;
    cursor: pointer;
    text-decoration: none;
    transition: color 0.25s ease;

    &:focus-visible {
      outline: 2px solid $color-primary;
      outline-offset: 4px;
    }

    &:hover {
      color: $color-text-muted;

      .hero__link-icon {
        transform: translate(3px, -3px);
      }
    }
  }

  &__link-text {
    font-family: $font-body;
    font-size: clamp(1.125rem, 1.5vw, 1.25rem);
    /* от 18px до 20px */
    font-weight: 400;
    line-height: 1.5;
  }

  &__link-icon {
    width: 1.125rem;
    /* 18px */
    height: 1.125rem;
    margin-left: 1rem;
    display: block;
    transform: translate(0, 0);
    transition: transform 0.25s cubic-bezier(0.25, 0.46, 0.45, 0.94);
  }

  &__image-wrapper {
    width: 100%;
    overflow: hidden;
    display: flex;
    justify-content: center;
  }

  &__image {
    width: 100%;
    max-width: 100vw;
    height: auto;
    object-fit: cover;
    display: block;

    // Ограничиваем минимальную высоту на смартфонах, чтобы картинка оставалась баннером, а не полоской
    @media (max-width: 480px) {
      min-height: 280px;
    }
  }
}
</style>
