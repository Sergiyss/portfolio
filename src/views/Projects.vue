<template>
  <section class="projects" id="projects">
    <div class="container">
      <h2 class="section-title">Мои проекты</h2>
      <div class="projects-grid">
        <div 
          class="project-card" 
          v-for="(project, index) in projects" 
          :key="index"
        >
          <img 
            class="project-img" 
            :src="`https://picsum.photos/600/350?random=${index}`"  
            :alt="project.title"
          >
          <div class="project-content">
            <h3 class="project-title">{{ project.title }}</h3>
            <p class="project-description">{{ project.description }}</p>
            <div class="project-tags">
              <span 
                class="project-tag" 
                v-for="(tag, tagIndex) in project.tags" 
                :key="tagIndex"
              >
                {{ tag }}
              </span>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
const projects = [
  {
    title: 'Корпоративный сайт для компании "БизнесПлюс"',
    description: 'Разработка корпоративного сайта на WordPress с интеграцией CRM и расширенными возможностями SEO.',
    tags: ['WordPress', 'CRM', 'SEO'],
    image: 'project1' // сюда ставь реальный путь к изображению или заглушку
  },
  {
    title: 'Интернет-магазин "Электроника+"',
    description: 'Разработка e-commerce платформы на WooCommerce с кастомным дизайном и системой онлайн-оплаты.',
    tags: ['WooCommerce', 'UX/UI', 'Online Payment'],
    image: 'project3'
  },
  {
    title: 'Промо-сайт стартапа "GreenTech"',
    description: 'Лендинг для стартапа по экологическим технологиям с фокусом на конверсию и мобильную адаптацию.',
    tags: ['Landing Page', 'Mobile First', 'Green Energy'],
    image: 'project2'
  }
]
</script>
