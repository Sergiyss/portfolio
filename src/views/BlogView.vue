<script setup>
import { ref, onMounted, computed } from 'vue';
import { useRoute } from 'vue-router';
import { useI18n } from 'vue-i18n';
import { projects } from '@/data/projects';
import Hero from '@/views/Hero.vue';
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

  <div v-if="project">
    <h1>{{ project.title }}</h1>
    <img :src="`https://picsum.photos/600/350?random=${project.id}`" :alt="project.title" class="w-full rounded-md" />
    <p>{{ project.description }}</p>
    <div class="tags">
      <span v-for="tag in project.tags" :key="tag" class="tag">{{ tag }}</span>
    </div>
  </div>
  <div v-else>
    <p>Проект не найден.</p>
  </div>
</template>


<style scoped>
.project {
  max-width: 800px;
  margin: 0 auto;
}
.project h1 {
  font-size: 2rem;
  font-weight: bold;
}
.project img {
  width: 100%;
  height: auto;
}
.project .tags {
  margin-top: 10px;
}
.project .tag {
  background-color: #f0f0f0;
  padding: 5px 10px;
  margin: 5px;
  border-radius: 5px;
}
</style>
