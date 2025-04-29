<script setup>
import { getImageUrl } from '@/utils/helpers';
import { getSvg } from '@/utils/helpers'; // Путь к вашей функции

import { useI18n } from 'vue-i18n';

const { t } = useI18n(); // подключаем $t для переводов

const skills = [
  {
    "name": "Java",
    "image": "icons8-java-96.png"
  },
  {
    "name": "kotlin",
    "image": "icons8-kotlin-96.png"
  },
  {
    "name": "Flutter",
    "image": "icons8-flutter-96.png"
  },
  {
    "name": "JavaScript",
    "image": "icons8-javascript-96.png"
  },
  {
    "name": "Vue.js",
    "image": "icons8-vue-js-96.png"
  },
  {
    "name": "PHP",
    "image": "icons8-php-80.png"
  },
  {
    "name": "WordPress",
    "image": "icons8-wordpress-96.png"
  },
  {
    "name": "git",
    "image": "icons8-git-96.png"
  },
  {
    "name": "Figma",
    "image": "icons8-figma-96.png"
  }
];

</script>

<template>
  <section class="py-16 bg-gray-100" id="about-me">
    <div class="container mx-auto px-4">

      <div class="relative inline-block w-50">
        <h2 class="about-title relative z-10">{{t('obout.title')}}</h2>
      </div>
      <div class="flex flex-col md:flex-row items-center md:items-start gap-10 mb-16">
        <div class="md:w-1/2">
          <div class="space-y-6 text-gray-700 text-lg leading-relaxed">
            <p class="obout-description" v-for="(paragraph, index) in t('obout.description').split('\n')" :key="index">
              {{ paragraph }}
            </p>
          </div>

          <h3 class="m-skills py-8">Skills</h3>
          <ul class="grid grid-cols-2 sm:grid-cols-3 gap-4 text-gray-600 text-base">
            <li v-for="(skill, index) in skills" :key="index" class="flex justify-center">
              <div class="flex flex-col items-center text-center gap-2">
                <img :src="getImageUrl(skill.image)" :alt="skill.name" class="w-24 h-24 object-contain" />
                <span>{{ skill.name }}</span>
              </div>
            </li>
          </ul>

        </div>

        <div class="md:w-1/2 flex justify-center">
          <img :src="getImageUrl('Image.png')" alt="Image" class="max-w-2xs h-auto">
        </div>
      </div>
    </div>
  </section>
</template>


<style scoped>

</style>