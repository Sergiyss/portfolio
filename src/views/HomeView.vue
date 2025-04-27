<script setup>
// Можно импортировать компоненты, если нужно
// import MyComponent from '@/components/MyComponent.vue';

// Используем $t для перевода (когда настроим i18n)
// import { useI18n } from 'vue-i18n';
// const { t } = useI18n();

// Управление <head> для SEO
import { useHead } from '@vueuse/head';
import Projects from '@/views/Projects.vue';
import Hero from '@/views/Hero.vue';
useHead({
  title: 'Главная | Мое Портфолио', // Динамический title
  meta: [
    { name: 'description', content: 'Портфолио веб-разработчика и мобильного разработчика...' },
    // Другие мета-теги (og:title, og:description и т.д.)
  ],
});
</script>

<template>
  <main>
    <Hero />
    <h1>{{ $t('home.title') }}</h1> {/* Пример использования перевода */}
    <p>Добро пожаловать на мой сайт-портфолио!</p>
    <Projects />
  </main>
</template>

<style scoped>
/* Стили только для этого компонента */
h1 {
  color: var(--text-color); /* Пример использования CSS переменной для темы */
}
</style>