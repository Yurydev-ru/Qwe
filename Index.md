# 🎨 Полная Дизайн-Система: SCSS & CSS-переменные

---

## 📦 Структура файлов

```plaintext
assets/
└── styles/
    ├── abstracts/
    │   ├── _variables.scss      // 🎨 CSS-переменные
    │   ├── _mixins.scss         // 🛠 Миксины
    │   ├── _media.scss          // 📱 Точки останова
    ├── base/
    │   ├── _reset.scss
    │   ├── _typography.scss
    ├── components/
    │   ├── _buttons.scss
    │   ├── _cards.scss
    └── main.scss                // 🌈 Главный SCSS
```

---

## 🧩 Переменные и Темизация

```scss
:root {
  /* Цветовая палитра — светлая тема */
  --color-primary: #01F2CF;
  --color-primary-light: #04D9AA;
  --color-primary-dark: #03D3DA;
  --color-secondary: #D72828;
  --color-accent: #FF8702;
  --color-info: #4861D0;
  --color-info-light: #59C2F4;
  --color-neutral-100: #FFFFFF;
  --color-neutral-900: #0D0D0D;
  --color-surface: #F2F2F2;
  --color-text-primary: #0D0D0D;
  --color-text-secondary: #4861D0;

  /* Типографика */
  --font-family-heading: 'Exo 2', sans-serif;
  --font-family-body: 'Exo 2', sans-serif;
  --font-weight-regular: 400;
  --font-weight-bold: 700;
  --font-size-base: 16px;
  --font-size-lg: 24px;
  --font-size-xl: 32px;

  /* Скругления и тени */
  --radius-sm: 8px;
  --radius-md: 16px;
  --shadow-sm: 0 2px 4px rgba(0, 0, 0, 0.1);
  --shadow-md: 0 4px 12px rgba(0, 0, 0, 0.15);
  --shadow-glow: 0 0 10px var(--color-primary);

  /* Пространства */
  --space-xs: 4px;
  --space-sm: 8px;
  --space-md: 16px;
  --space-lg: 24px;
  --space-xl: 32px;
}

/* 🌚 Тёмная тема */
[data-theme='dark'] {
  --color-surface: #1A1A1A;
  --color-text-primary: #FFFFFF;
  --color-text-secondary: #59C2F4;
  --shadow-glow: 0 0 8px var(--color-primary);
}
```

---

## ✍️ Типографика (`typography.scss`)

```scss
body {
  font-family: var(--font-family-body);
  font-weight: var(--font-weight-regular);
  font-size: var(--font-size-base);
  color: var(--color-text-primary);
  background-color: var(--color-surface);
}

h1, h2, h3, h4, h5 {
  font-family: var(--font-family-heading);
  font-weight: var(--font-weight-bold);
  color: var(--color-text-primary);
}

h1 { font-size: var(--font-size-xl); }
h2 { font-size: var(--font-size-lg); }
```

---

## 🔘 Кнопки (`buttons.scss`)

```scss
.button {
  display: inline-block;
  padding: var(--space-sm) var(--space-md);
  border-radius: var(--radius-sm);
  font-weight: var(--font-weight-bold);
  text-align: center;
  transition: all 0.3s ease;

  &--primary {
    background: var(--color-primary);
    color: var(--color-neutral-100);
    box-shadow: var(--shadow-glow);

    &:hover { background: var(--color-primary-dark); }
  }

  &--danger {
    background: var(--color-secondary);
    color: var(--color-neutral-100);

    &:hover { background: var(--color-accent); }
  }
}
```

---

## 🃏 Карточки (`cards.scss`)

```scss
.card {
  background-color: var(--color-surface);
  border-radius: var(--radius-md);
  padding: var(--space-md);
  box-shadow: var(--shadow-sm);
  transition: box-shadow 0.3s ease;

  &:hover { box-shadow: var(--shadow-md); }

  &__title {
    font-weight: var(--font-weight-bold);
    font-size: var(--font-size-lg);
  }
  &__description {
    font-size: var(--font-size-base);
    color: var(--color-text-secondary);
  }
}
```

---

## 🖼 Иконки (`icons.scss`)

```scss
.icon {
  width: 24px;
  height: 24px;
  fill: var(--color-text-secondary);
  transition: fill 0.2s ease;

  &--active {
    fill: var(--color-primary);
    box-shadow: var(--shadow-glow);
  }
}
```

---

## 📱 Адаптивность (`media.scss`)

```scss
$breakpoints: (
  "sm": 480px,
  "md": 768px,
  "lg": 1024px,
  "xl": 1280px,
);

@mixin respond($breakpoint) {
  @media (min-width: map-get($breakpoints, $breakpoint)) {
    @content;
  }
}
```

---

## 🧩 Использование в `main.scss`

```scss
@use 'abstracts/variables';
@use 'abstracts/mixins';
@use 'abstracts/media';
@use 'base/reset';
@use 'base/typography';
@use 'components/buttons';
@use 'components/cards';
```

---

## 🖼 Пример адаптивного компонента (`_cards.scss`)

```scss
.card {
  background-color: var(--color-surface);
  padding: var(--space-md);
  border-radius: var(--radius-md);
  box-shadow: var(--shadow-glow);

  @include respond(md) {
    padding: var(--space-lg);
  }

  &__title {
    font-size: var(--font-size-lg);
    @include respond(md) { font-size: var(--font-size-xl); }
  }
}
```

---

## ⚙️ Подключение SCSS в Nuxt

```ts
// nuxt.config.ts
export default defineNuxtConfig({
  css: ['@/assets/styles/main.scss']
})
```

---

## 🌗 Переключение тем

```ts
// composables/useTheme.ts
export const useTheme = () => {
  const toggle = () => {
    const current = document.documentElement.getAttribute('data-theme')
    const next = current === 'dark' ? 'light' : 'dark'
    document.documentElement.setAttribute('data-theme', next)
  }
  return { toggle }
}
```

---

## 🌓 Компонент для темы (`ThemeToggle.vue`)

```vue
<template>
  <button class="button button--primary" @click="toggle">
    {{ isDark ? 'Светлая тема' : 'Тёмная тема' }}
  </button>
</template>
<script setup lang="ts">
const isDark = ref(false)
const toggle = () => {
  isDark.value = !isDark.value
  document.documentElement.setAttribute('data-theme', isDark.value ? 'dark' : 'light')
}
</script>
<style scoped>
.button { cursor: pointer; }
</style>
```

---

## 🏠 Пример страницы (`pages/index.vue`)

```vue
<template>
  <section class="page">
    <ThemeToggle />
    <h1 class="hero__title">Привет, я веб-дизайнер</h1>
    <p class="hero__desc">Я создаю современные сайты с адаптивным интерфейсом и уникальным стилем.</p>
    <div class="card">
      <h2 class="card__title">Проект A</h2>
      <p class="card__description">Кейс, в котором я реализовал сложную анимацию и темную тему на SCSS.</p>
    </div>
  </section>
</template>

<script setup lang="ts">
import ThemeToggle from '~/components/ThemeToggle.vue'
</script>

<style scoped>
.page {
  max-width: 720px;
  margin: 0 auto;
  padding: var(--space-lg);
  background: var(--color-bg);
  color: var(--color-text);
}
.hero__title { font-size: var(--font-size-xl); margin-bottom: var(--space-sm); }
.hero__desc { color: var(--color-text-muted); margin-bottom: var(--space-lg); }
</style>
```

---

## ⚡️ Автоматическая тема при загрузке (`app.vue`)

```vue
<script setup>
onMounted(() => {
  const theme = window.matchMedia('(prefers-color-scheme: dark)').matches ? 'dark' : 'light'
  document.documentElement.setAttribute('data-theme', theme)
})
</script>
```

---

## 🌈 Фоновая стилизация и плавные переходы

```scss
html {
  transition: background-color 0.3s ease, color 0.3s ease;
  scroll-behavior: smooth;
}
```

---

## 🖋 Подключение шрифта Exo 2

```html
<!-- В app.vue или app.html -->
<link
  href="https://fonts.googleapis.com/css2?family=Exo+2:wght@400;600;700&display=swap"
  rel="stylesheet"
/>
```

```scss
:root {
  --font-family: 'Exo 2', sans-serif;
}
```

---

## 🖼 Layout (`layouts/default.vue`)

```vue
<template>
  <div class="layout">
    <header class="header">
      <nav>
        <NuxtLink to="/">Главная</NuxtLink>
        <NuxtLink to="#about">Обо мне</NuxtLink>
        <NuxtLink to="#projects">Проекты</NuxtLink>
        <NuxtLink to="#contact">Контакты</NuxtLink>
      </nav>
      <ThemeToggle />
    </header>
    <main><slot /></main>
    <footer class="footer">© {{ new Date().getFullYear() }} Мой сайт</footer>
  </div>
</template>
<script setup lang="ts">
import ThemeToggle from '~/components/ThemeToggle.vue'
</script>
<style scoped>
.header, .footer {
  padding: var(--space-md);
  background-color: var(--color-surface);
  color: var(--color-text);
  display: flex;
  justify-content: space-between;
  align-items: center;
}
nav a {
  margin-right: var(--space-sm);
  text-decoration: none;
  color: var(--color-text-muted);
}
</style>
```

---

## 💎 Адаптивность (если нужно усилить)

```scss
@mixin mobile {
  @media (max-width: 768px) { @content; }
}
.card {
  padding: var(--space-lg);
  @include mobile { padding: var(--space-md); }
}
```

---

## 🚀 Готово!

- Полноценный layout  
- 3 секции для сайта-портфолио  
- Темизация через CSS-переменные  
- SCSS-структура  
- Адаптивность  
- Красивая типографика и яркие акценты 🎉

---

**Используй этот шаблон как мощную основу для современного, яркого и крутого веб-дизайна!**
