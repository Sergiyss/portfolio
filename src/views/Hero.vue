<template>
    <section class="hero">
      <div class="container">
        <img  class="image_hero" :src="getImageUrl('Memoji round.png')" alt="Hero Image" />
        <h1>{{ t('hero.title') }}</h1>
        <p>{{ hero.subtitle }}</p>
      </div>
    </section>
  </template>
  
  <script setup>
  import { useI18n } from 'vue-i18n';
  
  const { t } = useI18n(); // подключаем $t для переводов
  
  const hero = {
    get title() {
      return t('hero.title');
    },
    get subtitle() {
      return t('hero.subtitle');
    },
    get cta() {
      return t('hero.cta');
    }
  };
  
  function scrollToContact() {
    const element = document.getElementById('contact');
    if (element) {
      element.scrollIntoView({ behavior: 'smooth' });
    }
  }

  function getImageUrl(name) {
    return new URL(`../assets/images/${name}`, import.meta.url).href;
  }

  </script>
  