<template>
  <!-- Подвал сайта (Блок footer) -->
  <footer class="footer">
    <div class="footer__container container">

      <!-- Верхняя часть футера -->
      <div class="footer__top">
        <!-- Левый блок: Брендинг -->
        <div class="footer__brand">
          <a href="#" class="footer__logo">LuxuryDetails</a>
          <p class="footer__brand-text">
            Experience the prestige of a professionally detailed car,
            radiating elegance and refinement at every turn.
          </p>
        </div>

        <!-- Правый блок: Группа колонок навигации -->
        <div class="footer__nav">
          <div v-for="(column, colIndex) in navColumns" :key="colIndex" class="footer__column">
            <h4 class="footer__column-title">{{ column.title }}</h4>
            <ul class="footer__list">
              <li v-for="(link, linkIndex) in column.links" :key="linkIndex">
                <!-- Обычные якорные ссылки -->
                <a v-if="!link.isExternal" :href="link.href" class="footer__link">
                  {{ link.label }}
                </a>
                <!-- Внешние ссылки на соцсети -->
                <a v-else :href="link.href" target="_blank" rel="noopener noreferrer" class="footer__link">
                  {{ link.label }}
                </a>
              </li>
            </ul>
          </div>
        </div>
      </div>

      <!-- Декоративная разделительная БЭМ-линия -->
      <div class="footer__line" aria-hidden="true"></div>

      <!-- Нижняя часть футера (Копирайт и юридические ссылки) -->
      <div class="footer__bottom">
        <!-- Автоматический динамический текущий год -->
        <p class="footer__copyright">LuxuryDetails © {{ currentYear }}</p>
        <div class="footer__legal">
          <a v-for="(legal, index) in legalLinks" :key="index" :href="legal.href" class="footer__legal-link">
            {{ legal.label }}
          </a>
        </div>
      </div>

    </div>
  </footer>
</template>

<script setup>
// Вычисляем текущий год автоматически, чтобы сайт всегда оставался актуальным
const currentYear = new Date().getFullYear()

// Массив данных колонок меню для v-for
const navColumns = [
  {
    title: 'Website',
    links: [
      { label: 'Services', href: '#services' },
      { label: 'Pricing', href: '#pricing' },
      { label: 'About', href: '#about' }
    ]
  },
  {
    title: 'Contact',
    links: [
      { label: 'Get a quote', href: '#quote' },
      { label: 'Contact form', href: '#contact' },
      { label: 'Email us', href: 'mailto:info@luxuredetails.com' }
    ]
  },
  {
    title: 'Social Media',
    links: [
      { label: 'Facebook', href: '#facebook', isExternal: true },
      { label: 'Instagram', href: '#instagram', isExternal: true },
      { label: 'Twitter', href: '#twitter', isExternal: true },
      { label: 'Youtube', href: '#youtube', isExternal: true }
    ]
  }
]

// Массив для юридических ссылок внизу
const legalLinks = [
  { label: 'Cookie policy', href: '#cookie' },
  { label: 'Terms of service', href: '#terms' },
  { label: 'Privacy policy', href: '#privacy' }
]
</script>

<style lang="scss" scoped>
@use '../assets/styles/variables' as *;

.footer {
  width: 100%;
  background-color: $color-bg;
  padding-top: 2.5rem;
  padding-bottom: 4rem;

  @include tablet {
    padding-top: 3.75rem;
  }

  /* Верхний ряд */
  &__top {
    display: flex;
    align-items: flex-start;
    justify-content: space-between;
    // Десктопный отступ 14rem (224px) плавно уменьшается до 2rem на ноутбуках
    gap: clamp(2rem, 10vw, 14rem);
    margin-bottom: clamp(3rem, 6vw, 5rem);
    /* Отступ до линии */
    width: 100%;

    @include tablet {
      flex-direction: column;
      gap: 3rem;
    }
  }

  /* Левая колонка брендинга */
  &__brand {
    flex: 0 1 25rem;
    /* Ограничиваем ширину описания (400px) */
    width: 100%;

    @include tablet {
      flex: 0 1 100%;
      text-align: center;
    }
  }

  &__logo {
    display: inline-block;
    font-family: $font-title;
    font-size: 1.25rem;
    /* 20px */
    line-height: 1.5;
    /* 30px */
    font-weight: 500;
    color: $color-primary;
    margin-bottom: 2rem;
    /* 32px */
    text-decoration: none;

    @include tablet {
      margin-bottom: 1.5rem;
    }
  }

  &__brand-text {
    font-family: $font-body;
    font-size: 1rem;
    /* 16px */
    line-height: 1.375rem;
    /* 22px */
    font-weight: 400;
    color: $color-text-muted;
  }

  /* Правый блок с тремя колонками */
  &__nav {
    display: flex;
    align-items: flex-start;
    gap: clamp(2rem, 5vw, 4rem);
    /* 64px плавно сжимается */
    justify-content: flex-end;
    width: 100%;

    @include tablet {
      flex-direction: column;
      gap: 2.5rem;
      align-items: center;
      text-align: center;
    }
  }

  &__column {
    display: flex;
    flex-direction: column;
    min-width: max-content;

    @include tablet {
      align-items: center;
    }
  }

  /* Заголовок колонки (Website, Contact...) */
  &__column-title {
    font-family: $font-body;
    font-size: 1rem;
    /* 16px */
    line-height: 1.875rem;
    /* 30px */
    font-weight: 500;
    color: $color-text-muted;
    /* Серый цвет заголовков списков */
    margin-bottom: 2rem;
    /* 32px */

    @include tablet {
      margin-bottom: 1.25rem;
    }
  }

  &__list {
    display: flex;
    flex-direction: column;
    gap: 1.5rem;
    list-style: none;
    padding: 0;
    margin: 0;

    @include tablet {
      gap: 1rem;
    }
  }

  /* Ссылки меню футера */
  &__link {
    font-family: $font-body;
    font-size: 1rem;
    /* 16px */
    line-height: 1.875rem;
    /* 30px */
    font-weight: 500;
    color: $color-primary;
    white-space: nowrap;
    display: inline-block;
    text-decoration: none;
    transition: opacity 0.25s ease;

    &:hover {
      opacity: 0.7;
    }

    &:focus-visible {
      outline: 2px solid $color-primary;
      outline-offset: 4px;
    }
  }

  /* Нижняя горизонтальная линия */
  &__line {
    width: 100%;
    height: 1px;
    background-color: rgba($color-primary, 0.25);
    /* Тонкая линия 25% */
    margin-bottom: clamp(2rem, 5vw, 4rem);
    /* Отступ до копирайта */

    @include tablet {
      margin-bottom: 1.5rem;
    }
  }

  /* Самый нижний ряд футера */
  &__bottom {
    display: flex;
    align-items: center;
    justify-content: space-between;
    width: 100%;

    @include tablet {
      flex-direction: column-reverse;
      gap: 1.5rem;
      text-align: center;
    }
  }

  &__copyright {
    font-family: $font-body;
    font-size: 1rem;
    color: $color-primary;
    line-height: 1.5;
  }

  /* Контейнер для юридических ссылок */
  &__legal {
    display: flex;
    align-items: center;
    gap: 2rem;

    @include tablet {
      flex-direction: column;
      gap: 1rem;
    }
  }

  &__legal-link {
    font-family: $font-title;
    font-size: 1rem;
    /* 16px */
    line-height: 1.875rem;
    /* 30px */
    font-weight: 500;
    color: $color-primary;
    text-decoration: none;
    transition: color 0.25s ease;

    &:hover {
      color: rgba($color-primary, 0.25);
      /* Мягкое приглушение до 25% */
    }

    &:focus-visible {
      outline: 2px solid $color-primary;
      outline-offset: 4px;
    }
  }
}
</style>
