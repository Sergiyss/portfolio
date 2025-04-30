<template>
  <section class="projects" id="projects">
    <div class="container mx-auto px-4 py-8">
      <h2
          class="section-title text-center pt-8"
          v-html="t('project.title').replace(/\n/g, '<br>')"
      />

      <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-8 pt-8">
        <div
            class="project-card bg-white rounded-lg overflow-hidden shadow-lg hover:shadow-xl transform transition-all duration-300"
            v-for="(project, index) in projects"
            :key="index"
        >
          <router-link
              :to="{ path: '/blog', query: { id: project.id } }"
              class="block"
          >
            <div class="card-inner">
              <img
                  class="project-img w-full h-48 object-cover"
                  :src="getImageUrl(project.image)"
                  :alt="project.title"
              />

              <div class="project-content p-4">
                <h3 class="project-title text-xl font-semibold mb-2">{{ project.title }}</h3>


                <hr class="my-2 border-t border-gray-300"/>

                <p class="project-description text-gray-700 mb-4">
                  {{ project.description }} </p>
                <div class="project-tags mb-2">
                  <span
                      class="project-tag inline-block bg-gray-200 text-gray-700 text-sm px-2 py-1 rounded mr-2 mb-2"
                      v-for="(tag, tagIndex) in project.tags"
                      :key="tagIndex"
                  >
                    {{ tag }}
                  </span>
                </div>
                <div class="project-links flex justify-between text-blue-600 text-sm">
                  <!-- Отображение ссылки на GitHub если она есть -->
                  <span v-if="project.github">
                    <a :href="project.github" target="_blank" class="hover:underline">GitHub 🔗</a>
                  </span>

                  <!-- Отображение ссылки на Deploy если она есть -->
                  <span v-if="project.link">
                    <a :href="project.link" target="_blank" class="rounded text-white bg-amber-500 p-1 hover:underline">Play Market</a>
                  </span>
                </div>
              </div>
            </div>
          </router-link>
        </div>
      </div>

      <h2
          class="section-title text-center pt-8"
          v-html="t('project.title_site').replace(/\n/g, '<br>')"
      />
      <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-8 pt-8">
        <div
            class="project-card bg-white rounded-lg overflow-hidden shadow-lg hover:shadow-xl transform transition-all duration-300"
            v-for="(project, index) in web_projects"
            :key="index"
        >
<!--          <router-link-->
<!--              :to="{ path: '/blog', query: { id: project.id } }"-->
<!--              class="block"-->
<!--          >-->
            <div class="card-inner">
              <img
                  class="project-img w-full h-48 object-cover"
                  :src="getImageUrl(project.image)"
                  :alt="project.title"
              />

              <div class="project-content p-4">
                <h3 class="project-title text-xl font-semibold mb-2">{{ project.title }}</h3>

                <p class="project-description text-gray-700 mb-4">
                  {{ project.description }}
                </p>

                <hr class="my-2 border-t border-gray-300"/>

                <p
                    class="project-description text-gray-700 mb-4"
                    v-html="project.fullDescription.replace(/\n/g, '<br>')"
                />

                <div class="project-tags mb-2">
                  <span
                      class="project-tag inline-block bg-gray-200 text-gray-700 text-sm px-2 py-1 rounded mr-2 mb-2"
                      v-for="(tag, tagIndex) in project.tags"
                      :key="tagIndex"
                  >
                    {{ tag }}
                  </span>
                </div>


                <div class="project-links flex justify-between text-blue-600 text-sm">
                  <!-- Отображение ссылки на GitHub если она есть -->
                  <span v-if="project.github">
                    <a :href="project.github" target="_blank" class="hover:underline">GitHub 🔗</a>
                  </span>

                  <!-- Отображение ссылки на Deploy если она есть -->
                  <span v-if="project.link">
                    <a :href="project.link" target="_blank" class="rounded text-white bg-amber-500 p-1 hover:underline">Play Market</a>
                  </span>
                </div>
              </div>
            </div>
<!--          </router-link>-->
        </div>
      </div>
    </div>
  </section>
</template>



<script setup>
  import {ref, computed} from 'vue'
  import { projects } from '@/data/projects';
  import { web_projects } from '@/data/web_projects';
  import {useI18n} from 'vue-i18n';
  import { getImageUrl } from '@/utils/helpers';

  const {t} = useI18n(); // подключаем $t для переводов

  const itemsPerPage = ref(getItemsPerPage())
  const currentPage = ref(0)

  function getItemsPerPage() {
    return window.innerWidth < 768 ? 1 : 3 // 1 на мобилке, 6 на десктопе
  }

  window.addEventListener('resize', () => {
    itemsPerPage.value = getItemsPerPage()
    currentPage.value = 0
  })
</script>

<style scoped>
.project-card {
  display: flex;
  flex-direction: column;
}

.card-inner:hover {
  transform: translateY(-5px);
}

.project-img {
  width: 100%;
  height: auto;
}

.project-content {
  padding: 1rem;
}

.project-title {
  font-size: 1.1rem;
  margin-bottom: 0.5rem;
}

.project-tags {
  display: flex;
  flex-wrap: wrap;
  gap: 0.4rem;
  margin-bottom: 0.5rem;
}


@media (max-width: 767px) {
  .card-inner {
    width: 100%;
    box-sizing: border-box;
  }
}

</style>