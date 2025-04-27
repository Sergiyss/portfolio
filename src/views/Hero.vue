<template>
    <section class="hero">
      <div class="container">
        <h1>{{ t('hero.title') }}</h1>
        <p>{{ hero.subtitle }}</p>
        <button class="cta-button" @click="scrollToContact">
          {{ hero.cta }}
        </button>
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
  </script>
  