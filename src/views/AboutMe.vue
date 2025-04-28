<script setup>
import { getImageUrl } from '@/utils/helpers';
import { useI18n } from 'vue-i18n';

const { t } = useI18n(); // подключаем $t для переводов

const skills = [
  'HTML',
  'CSS',
  'JavaScript',
  'Vue.js',
  'React',
  'Node.js',
  'Git',
  'Responsive Design',
  'SEO'
];

</script>

<template>
  <section class="about-me" id="about-me">
    <div class="container">


      <h2 class="section-title">Обо мне</h2>
      <div class="row">
        <div class="about-me-content">
          <div class="about-me-text">
            <p>Я веб-разработчик с опытом работы более 5 лет. Специализируюсь на создании адаптивных и высокопроизводительных веб-приложений.</p>
            <p>Мои навыки включают HTML, CSS, JavaScript, Vue.js, React и другие современные технологии.</p>
          </div>
        </div>
        <img :src="getImageUrl('Image.png')" alt="Image" />
      </div>
      <div class="about-me-skills">
        <h3>Мои навыки</h3>
        <ul>
          <li v-for="(skill, index) in skills" :key="index">{{ skill }}</li>
        </ul>
      </div>
    </div>
  </section>
</template>

<style scoped>

</style>