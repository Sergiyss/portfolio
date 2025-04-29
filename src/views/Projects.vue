<template>
  <section class="projects" id="projects">
    <div class="container">
      <h2 class="section-title">{{ t('project.title') }}</h2>

      <div class="carousel-wrapper">
        <div class="carousel-window">

          <div
              class="carousel-track"
              :style="{ transform: `translateX(-${currentPage * 100}%)` }"
          >
            <div
                class="carousel-page"
                v-for="(page, pageIndex) in paginatedProjects"
                :key="pageIndex"
            >
              <div
                  class="project-card"
                  v-for="(project, index) in page"
                  :key="index"
              >
                <router-link
                    :to="{ path: '/blog', query: { id: project.id } }"
                    class="carousel-track block"
                    :style="{ transform: `translateX(-${currentPage * 100}%)` }"
                >
                  <div class="card-inner">
                    <img
                        class="project-img"
                        :src="`https://picsum.photos/600/350?random=${index}`"
                        :alt="project.title"
                    />
                    <div class="project-content">
                      <h3 class="project-title">{{ project.title }}</h3>
                      <div class="project-tags">
                      <span
                          class="project-tag"
                          v-for="(tag, tagIndex) in project.tags"
                          :key="tagIndex">
                        {{ tag }}
                      </span>
                      </div>
                      <div class="project-links">
                        <span>GitHub 🔗</span>
                        <span>Deploy 🚀</span>
                      </div>
                    </div>
                  </div>
                </router-link>
              </div>
            </div>
          </div>
        </div>

        <!-- Навигация -->
        <div class="carousel-controls flex justify-end gap-4">
          <div
              class="nav-circle flex items-center justify-center"
              @click="prevPage"
              :disabled="currentPage >= maxPage"
          >
            <img
                :src="getSvg('left')"
                alt="Arrow Icon"
                class="w-8 h-4 opacity-90 pointer-events-none"
            />
          </div>
          <div
              class="nav-circle flex items-center justify-center"
              @click="nextPage"
              :disabled="currentPage >= maxPage"
          >
            <img
                :src="getSvg('right')"
                alt="Arrow Icon"
                class="w-8 h-4 opacity-90 pointer-events-none"
            />
          </div>
        </div>

      </div>
    </div>
  </section>
</template>


<script setup>
import {ref, computed} from 'vue'
import {getSvg} from '@/utils/helpers';
import { projects } from '@/data/projects';
import {useI18n} from 'vue-i18n';

const {t} = useI18n(); // подключаем $t для переводов

const itemsPerPage = ref(getItemsPerPage())
const currentPage = ref(0)

function getItemsPerPage() {
  return window.innerWidth < 768 ? 1 : 3 // 1 на мобилке, 6 на десктопе
}

const paginatedProjects = computed(() => {
  const pages = []
  for (let i = 0; i < projects.length; i += itemsPerPage.value) {
    pages.push(projects.slice(i, i + itemsPerPage.value))
  }
  return pages
})

const maxPage = computed(() => paginatedProjects.value.length - 1)

function prevPage() {
  if (currentPage.value > 0) currentPage.value--
}

function nextPage() {
  if (currentPage.value < maxPage.value) currentPage.value++
}

window.addEventListener('resize', () => {
  itemsPerPage.value = getItemsPerPage()
  currentPage.value = 0
})
</script>

<style scoped>


.carousel-window {
  overflow: hidden;
  width: 100%;
}

.carousel-track {
  display: flex;
  transition: transform 0.5s ease-in-out;
  width: 100%;
}

.carousel-page {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-template-rows: repeat(2, auto);
  gap: 1rem;
  min-width: 100%;
  padding: 1rem 0;
}

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

.nav-circle {
  width: 40px;
  height: 40px;
  font-size: 1.5rem;
  border-radius: 50%;
  background: #f4b400;
  color: #fff;
  border: none;
  cursor: pointer;
}

.nav-circle:disabled {
  opacity: 0.4;
  cursor: not-allowed;
}


@media (max-width: 767px) {
  .carousel-page {
    grid-template-columns: 1fr;
  }

  .card-inner {
    width: 100%; /* ✅ Обязательно */
    box-sizing: border-box;
  }
}

</style>