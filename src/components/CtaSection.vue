<template>
  <!-- Финальная секция призыва к действию (Блок cta) -->
  <section class="cta" id="contact" aria-label="Sign up for detailing">
    <div class="cta__container container">
      <div class="cta__body">

        <!-- Адаптивный фон баннера (Retina ready) -->
        <picture class="cta__picture">
          <source srcset="
              ../assets/images/cta-bg.webp    1x,
              ../assets/images/cta-bg@2x.webp 2x
            " type="image/webp" />
          <source srcset="
              ../assets/images/cta-bg.png    1x,
              ../assets/images/cta-bg@2x.png 2x
            " />
          <img src="../assets/images/cta-bg.png" alt="Premium car at a detailing center" class="cta__img" loading="lazy"
            decoding="async" />
        </picture>

        <!-- Текстовый контент баннера -->
        <div class="cta__content">
          <h2 class="cta__title">Book your luxury car detailing today</h2>
          <p class="cta__text">
            Click the link bellow. Fill out the details and we’ll get back
            to you in less than 24 hours.
          </p>

          <!-- Ссылка со стрелочкой ↗ -->
          <a href="#booking-form" class="cta__link" aria-label="Submit a detailing request">
            <span class="cta__link-text">Get a quote now</span>
            <span class="cta__link-arrow-wrap">
              <svg class="cta__link-arrow" width="18" height="18" viewBox="0 0 18 18" fill="none" aria-hidden="true">
                <path
                  d="M17.707 1C17.707 0.447715 17.2593 0 16.707 0H7.70703C7.15475 0 6.70703 0.447715 6.70703 1C6.70703 1.55228 7.15475 2 7.70703 2H15.707V10C15.707 10.5523 16.1547 11 16.707 11C17.2593 11 17.707 10.5523 17.707 10V1ZM1.41414 17.7071L17.4141 1.70711L15.9999 0.292893L-7.55191e-05 16.2929L1.41414 17.7071Z"
                  fill="currentColor" />
              </svg>
            </span>
          </a>
        </div>

      </div>
    </div>
  </section>
</template>

<script setup>
// Логика пока не требуется
</script>

<style lang="scss" scoped>
@use '../assets/styles/variables' as *;

.cta {
  width: 100%;
  background-color: $color-bg;
  padding-top: clamp(3.75rem, 6vw, 6.25rem);
  /* от 60px до 100px */
  padding-bottom: clamp(2.5rem, 4vw, 3.75rem);

  &__body {
    position: relative;
    width: 100%;
    // Высота баннера: резиновая от 400px на мобилках до 500px на десктопе
    height: clamp(25rem, 35vw, 31.25rem);
    border-radius: 1rem;
    /* 16px */
    overflow: hidden;
    display: flex;
    align-items: flex-start;
    // Резиновые внутренние отступы шторки
    padding: clamp(3rem, 6vw, 5rem) clamp(1.5rem, 6vw, 5rem);

    @include tablet {
      height: auto;
      /* На планшетах и мобилках баннер растет по высоте контента */
      align-items: center;
      justify-content: center;
      text-align: center;
    }

    /* Затемняющий оверлей */
    &::after {
      content: '';
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background: rgba(0, 0, 0, 0.25);
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

  &__content {
    position: relative;
    z-index: 3;
    display: flex;
    flex-direction: column;

    @include tablet {
      align-items: center;
    }
  }

  &__title {
    font-family: $font-title;
    font-size: clamp(2.25rem, 4vw, 3rem);
    /* Резиновый заголовок 36px-48px */
    line-height: 1.125;
    color: $color-primary;
    max-width: 26.5625rem;
    /* 425px */
    margin-bottom: clamp(1.5rem, 3vw, 2.5rem);

    @include tablet {
      max-width: 100%;
    }
  }

  &__text {
    font-family: $font-body;
    font-size: 1rem;
    line-height: 1.5;
    font-weight: 400;
    color: $color-text-light-grey;
    max-width: 21.75rem;
    /* 348px */
    margin-bottom: clamp(2rem, 4vw, 3rem);

    @include tablet {
      max-width: 100%;
    }
  }

  &__link {
    display: inline-flex;
    align-items: center;
    gap: 1rem;
    font-family: $font-body;
    font-size: clamp(1.125rem, 1.5vw, 1.25rem);
    /* от 18px до 20px */
    line-height: 1.5;
    font-weight: 500;
    color: rgba($color-primary, 0.7);
    width: max-content;
    text-decoration: none;
    transition: color 0.4s cubic-bezier(0.25, 1, 0.5, 1);

    &:hover {
      color: $color-primary;

      .cta__link-arrow-wrap {
        transform: translate(4px, -4px);
        /* Идеально плавная стрелка */
      }
    }

    &:focus-visible {
      outline: 2px solid $color-primary;
      outline-offset: 4px;
    }

    &-arrow-wrap {
      display: inline-block;
      width: 1.125rem;
      /* 18px */
      height: 1.125rem;
      flex-shrink: 0;
      transition: transform 0.4s cubic-bezier(0.25, 1, 0.5, 1);
    }

    &-arrow {
      display: block;
      width: 100%;
      height: 100%;
    }
  }
}
</style>
