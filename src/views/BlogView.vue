<script setup>
import { ref, onMounted, computed } from 'vue';
import { useRoute } from 'vue-router';
import { useI18n } from 'vue-i18n';
import { projects } from '@/data/projects';
import Hero from '@/views/Hero.vue';
import BottomBar from '@/views/BottomBar.vue';
import { getImageUrl } from '@/utils/helpers';

const { t } = useI18n();
const route = useRoute();

const projectId = ref(null);
const project = ref(null);

onMounted(() => {
  projectId.value = Number(route.query.id);
  project.value = projects.find(p => p.id === projectId.value);

  if (!project.value) {
    console.log('Проект не найден!');
  }
});

// computed заголовок
const projectTitle = computed(() => project.value?.title ?? '');
</script>

<template>
  <Hero
      title="Блог"
      :subtitle="projectTitle"
      image="Memoji round.png"
      :showImage="false"
  />

  <div v-if="project" class="project-wrapper">
    <div class="project-content">
      <img
          :src="`https://picsum.photos/600/350?random=${project.id}`"
          :alt="project.title"
          class="project-image"
      />

      <h1 class="project-title">{{ project.title }}</h1>
      <div class="project-description">
        <p v-for="(paragraph, index) in project.fullDescription.split('\n')" :key="index">
          {{ paragraph }}
        </p>
      </div>

      <div class="tags">
        <span v-for="tag in project.tags" :key="tag" class="tag">{{ tag }}</span>
      </div>
    </div>
  </div>

  <div v-else class="not-found">
    <p>Проект не найден.</p>
  </div>

  <BottomBar />
</template>


<style scoped>
.project-wrapper {
  display: flex;
  justify-content: center;
  padding: 2rem 1rem;
  background-color: #f9f9f9;
}

.project-content {
  max-width: 920px;
  width: 100%;
  background: white;
  border-radius: 12px;
  box-shadow: 0 4px 12px rgba(0,0,0,0.05);
  padding: 2rem;
}

.project-image {
  width: 100%;
  max-height: 350px;
  object-fit: cover;
  border-radius: 8px;
  margin-bottom: 1.5rem;
}

.project-title {
  font-size: 2rem;
  font-weight: bold;
  margin-bottom: 1rem;
}

.project-description {
  font-size: 1.125rem;
  line-height: 1.8;
  margin-bottom: 1.5rem;
  color: #333;
}

.tags {
  display: flex;
  flex-wrap: wrap;
  gap: 0.5rem;
}

.tag {
  background-color: #eef1f6;
  color: #333;
  padding: 0.4rem 0.8rem;
  border-radius: 20px;
  font-size: 0.875rem;
}
</style>
