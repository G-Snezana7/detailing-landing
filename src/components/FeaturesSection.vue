<template>
  <!-- Секция преимуществ (Блок features) -->
  <section class="features" id="features" aria-labelledby="features-title">
    <div class="features__container container">

      <!-- Левая колонка: Заголовок и изображение машины -->
      <div class="features__left">
        <h2 id="features-title" class="features__title">
          We will take good care of your car
        </h2>
        <div class="features__image-wrapper">
          <picture>
            <source srcset="
                ../assets/images/features-car.webp    1x,
                ../assets/images/features-car@2x.webp 2x
              " type="image/webp" />
            <source srcset="
                ../assets/images/features-car.png    1x,
                ../assets/images/features-car@2x.png 2x
              " />
            <img src="../assets/images/features-car.png" alt="A premium car in a detailing studio" class="features__img"
              loading="lazy" decoding="async" />
          </picture>
        </div>
      </div>

      <!-- Вертикальная линия-разделитель (Скрывается на мобильных) -->
      <div class="features__divider" aria-hidden="true"></div>

      <!-- Правая колонка: Список преимуществ и ссылка -->
      <div class="features__right">
        <ul class="features__list">
          <li v-for="(item, index) in featureItems" :key="index" class="features__item feature-item">
            <!-- Иконка вставляется динамически -->
            <div class="feature-item__icon-wrapper" v-html="item.icon"></div>

            <div class="feature-item__content">
              <h3 class="feature-item__title">{{ item.title }}</h3>
              <p class="feature-item__text">{{ item.text }}</p>
            </div>
          </li>
        </ul>

        <!-- Ссылка со стрелочкой ↗ внизу списка -->
        <a href="#contact" class="features__link">
          <span>Get a quote now</span>
          <span class="features__link-arrow-wrap">
            <svg class="features__link-arrow" width="18" height="18" viewBox="0 0 18 18" fill="none" aria-hidden="true">
              <path
                d="M17.707 1C17.707 0.447715 17.2593 0 16.707 0H7.70703C7.15475 0 6.70703 0.447715 6.70703 1C6.70703 1.55228 7.15475 2 7.70703 2H15.707V10C15.707 10.5523 16.1547 11 16.707 11C17.2593 11 17.707 10.5523 17.707 10V1ZM1.41414 17.7071L17.4141 1.70711L15.9999 0.292893L-7.55191e-05 16.2929L1.41414 17.7071Z"
                fill="currentColor" />
            </svg>
          </span>
        </a>
      </div>

    </div>
  </section>
</template>

<script setup>

const featureItems = [
  {
    title: 'Precise work',
    text: 'We uphold the highest standards of professionalism when servicing your vehicles.',
    icon: `<svg width="24" height="24" viewBox="0 0 24 24" fill="none"><g><path d="M23.0625 11.0625H22.1132C21.671 6.20006 17.799 2.32889 12.9375 1.88677V0.9375C12.9375 0.419719 12.5178 0 12 0C11.4822 0 11.0625 0.419719 11.0625 0.9375V1.88677C6.20006 2.32898 2.32889 6.20095 1.88681 11.0625H0.9375C0.419719 11.0625 0 11.4822 0 12C0 12.5178 0.419719 12.9375 0.9375 12.9375H1.88681C2.32898 17.7999 6.20095 21.6711 11.0625 22.1132V23.0625C11.0625 23.5803 11.4822 24 12 24C12.5178 24 12.9375 23.5803 12.9375 23.0625V22.1132C17.7999 21.671 21.6711 17.799 22.1132 12.9375H23.0625C23.5803 12.9375 24 12.5178 24 12C24 11.4822 23.5803 11.0625 23.0625 11.0625ZM12.9375 20.2279V19.375C12.9375 18.8573 12.5178 18.4375 12 18.4375C11.4822 18.4375 11.0625 18.8573 11.0625 19.375V20.2279C7.24388 19.7956 4.20441 16.7561 3.77213 12.9375H4.62497C5.14275 12.9375 5.56247 12.5178 5.56247 12C5.56247 11.4822 5.14275 11.0625 4.62497 11.0625H3.77213C4.20441 7.24388 7.24388 4.20441 11.0625 3.77213V4.62497C11.0625 5.14275 11.4822 5.56247 12 5.56247C12.5178 5.56247 12.9375 5.14275 12.9375 4.62497V3.77213C16.7561 4.20441 19.7956 7.24388 20.2279 11.0625H19.375C18.8573 11.0625 18.4375 11.4822 18.4375 12C18.4375 12.5178 18.8573 12.9375 19.375 12.9375H20.2279C19.7956 16.7561 16.7561 19.7956 12.9375 20.2279ZM12 7.37498C9.44977 7.37498 7.37498 9.44977 7.37498 12C7.37498 14.5502 9.44977 16.625 12 16.625C14.5502 16.625 16.625 14.5502 16.625 12C16.625 9.44977 14.5502 7.37498 12 7.37498ZM12 14.75C10.4836 14.75 9.24998 13.5164 9.24998 12C9.24998 10.4836 10.4836 9.24998 12 9.24998C13.5164 9.24998 14.75 10.4836 14.75 12C14.75 13.5164 13.5164 14.75 12 14.75Z" fill="currentColor"/></g><defs><clipPath><rect width="24" height="24" fill="currentColor"/></clipPath></defs></svg>`
  },
  {
    title: 'Premium Products and Services',
    text: 'Ensure your car\'s longevity with a periodic exterior protection treatment.',
    icon: `<svg width="24" height="21" viewBox="0 0 24 21" fill="none"><path d="M23.7113 7.014L19.4249 0.726C19.1152 0.271406 18.6018 0 18.0515 0H5.9482C5.39789 0 4.88442 0.271406 4.57481 0.725859L0.287902 7.01461C-0.147473 7.65487 -0.0830664 8.5117 0.44048 9.078L10.7776 20.2742C11.4354 20.9894 12.566 20.9874 13.221 20.2752L23.5588 9.07837C24.063 8.53298 24.1636 7.67915 23.7113 7.014ZM6.52832 8.74345L10.1913 17.5661L2.04557 8.74345H6.52832ZM13.0136 1.40625L15.881 7.33716H8.11861L10.9859 1.40625H13.0136ZM15.9487 8.74345L11.9998 18.2547L8.05097 8.74341H15.9487V8.74345ZM17.4713 8.74345H21.954L13.8083 17.5661L17.4713 8.74345ZM18.2629 1.51795L22.2297 7.3372H17.443L14.5756 1.4063H18.0515C18.1362 1.40625 18.2152 1.44797 18.2629 1.51795ZM5.73684 1.51781C5.78442 1.44797 5.8634 1.4063 5.94815 1.4063H9.42403L6.55668 7.3372H1.7699L5.73684 1.51781Z" fill="currentColor"/></svg>`
  },
  {
    title: 'Bespoke Protection Pack',
    text: 'Every vehicle gets a personalized approach with premium level paint shield coatings.',
    icon: `<svg width="24" height="24" viewBox="0 0 24 24" fill="none"><g><path d="M22.0574 6.17962C22.0451 5.53166 22.0333 4.91953 22.0333 4.32734C22.0333 3.86341 21.6573 3.48728 21.1933 3.48728C17.6006 3.48728 14.8653 2.45479 12.5852 0.237924C12.259 -0.0792828 11.74 -0.0791708 11.4139 0.237924C9.13413 2.45479 6.39922 3.48728 2.80678 3.48728C2.34285 3.48728 1.96672 3.86341 1.96672 4.32734C1.96672 4.91964 1.95507 5.53199 1.94264 6.18007C1.8275 12.2101 1.66979 20.4686 11.7244 23.9538C11.8136 23.9847 11.9066 24.0001 11.9995 24.0001C12.0925 24.0001 12.1856 23.9847 12.2746 23.9538C22.33 20.4685 22.1726 12.2098 22.0574 6.17962ZM11.9996 22.2686C3.37646 19.1361 3.50684 12.2739 3.62254 6.21211C3.62949 5.8483 3.63621 5.4957 3.64091 5.15004C7.00564 5.00802 9.6963 3.98841 11.9996 1.98189C14.3032 3.98841 16.9943 5.00813 20.3593 5.15004C20.364 5.49559 20.3707 5.84797 20.3776 6.21155C20.4932 12.2735 20.6235 19.136 11.9996 22.2686Z" fill="currentColor"/><path d="M14.8924 9.08181L10.8378 13.1362L9.1076 11.406C8.77952 11.078 8.2476 11.078 7.91964 11.406C7.59157 11.7342 7.59157 12.266 7.91964 12.5941L10.2438 14.9182C10.4078 15.0822 10.6228 15.1642 10.8378 15.1642C11.0527 15.1642 11.2678 15.0822 11.4318 14.9182L16.0802 10.2699C16.4084 9.94181 16.4084 9.40989 16.0803 9.08193C15.7524 8.75385 15.2204 8.75374 14.8924 9.08181Z" fill="currentColor"/></g></svg>`
  }
]
</script>

<style lang="scss" scoped>
@use '../assets/styles/variables' as *;

.features {
  width: 100%;
  background-color: $color-bg;
  padding-top: clamp(3.75rem, 6vw, 6.25rem);
  padding-bottom: clamp(3.75rem, 6vw, 6.25rem);

  &__container {
    display: flex;
    align-items: flex-start;
    justify-content: space-between;
    width: 100%;

    @include tablet {
      flex-direction: column;
      gap: 3.5rem;
    }
  }

  /* Левая колонка */
  &__left {
    flex: 0 1 24.8125rem;
    /* 397px из Figma */
    width: 100%;

    @include tablet {
      flex: 0 1 100%;
      text-align: center;
    }
  }

  &__title {
    font-family: $font-title;
    font-size: clamp(2.25rem, 4vw, 3rem);
    /* Резиновый заголовок 36px-48px */
    line-height: 1.125;
    color: $color-primary;
    margin-bottom: clamp(2.5rem, 5vw, 4rem);
    /* 64px плавно сжимается на мобильных */
  }

  &__image-wrapper {
    width: 100%;
    border-radius: 12px;
    overflow: hidden;
  }

  &__img {
    width: 100%;
    height: auto;
    object-fit: contain;
    display: block;
  }

  /* Вертикальная линия-разделитель */
  &__divider {
    width: 1px;
    align-self: stretch;
    /* Растягивается на всю высоту */
    background-color: rgba($color-primary, 0.25);
    flex-shrink: 0;
    margin-left: auto;
    margin-right: clamp(2rem, 6vw, 7rem);
    /* 112px плавно уменьшается */

    @include tablet {
      display: none;
      /* Скрываем разделитель на мобилках */
    }
  }

  /* Правая колонка */
  &__right {
    flex: 0 0 28rem;
    /* 448px из Figma */
    display: flex;
    flex-direction: column;
    width: 100%;

    @include tablet {
      flex: 0 1 100%;
    }
  }

  &__list {
    display: flex;
    flex-direction: column;
    width: 100%;
    padding: 0;
    margin: 0;
  }
}

/* --- Независимый БЭМ-компонент фичи --- */
.feature-item {
  display: flex;
  align-items: flex-start;
  gap: 1rem;
  /* 16px */
  border-bottom: 1px solid rgba($color-primary, 0.25);
  padding-bottom: clamp(1.75rem, 3vw, 2.5rem);
  margin-bottom: clamp(1.75rem, 3vw, 2.5rem);

  &:last-child {
    border-bottom: none;
    padding-bottom: 0;
    margin-bottom: clamp(2.5rem, 5vw, 4rem);
    /* Отступ до кнопки Get a quote */
  }

  &__icon-wrapper {
    color: $color-primary;
    flex-shrink: 0;
    width: 1.5rem;
    /* 24px */
    height: 1.5rem;
    margin-top: 0.25rem;
    /* Идеальное центрирование с первой строкой текста */

    :deep(svg) {
      width: 100%;
      height: 100%;
      display: block;
    }
  }

  &__content {
    display: flex;
    flex-direction: column;
  }

  &__title {
    font-family: $font-title;
    font-size: clamp(1.25rem, 2vw, 1.5rem);
    /* от 20px до 24px */
    line-height: 1.2;
    color: $color-primary;
    margin-bottom: 1.25rem;
    /* ~20px */
  }

  &__text {
    font-family: $font-body;
    font-size: 1rem;
    line-height: 1.5;
    font-weight: 400;
    color: $color-text-light-grey;
  }
}

/* --- Ссылка со стрелочкой ↗ внизу --- */
.features__link {
  display: inline-flex;
  align-items: center;
  gap: 1rem;
  /* 16px /font-family: $font-body;font-size: 1.25rem; / 20px */
  line-height: 1.5;
  font-weight: 500;
  color: rgba($color-primary, 0.7);
  width: max-content;
  text-decoration: none;
  transition: color 0.4s cubic-bezier(0.25, 1, 0.5, 1);

  @include tablet {
    align-self: center;
    /* Центрируем ссылку на планшетах/смартфонах */
  }

  &:hover {
    color: $color-primary;

    .features__link-arrow-wrap {
      transform: translate(4px, -4px);
      /* Стрелка взлетает */
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
</style>