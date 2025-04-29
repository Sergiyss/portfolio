<script setup>
import { ref } from 'vue'
import { getImageUrl } from '@/utils/helpers';

import { useI18n } from 'vue-i18n';
const { t } = useI18n(); // подключаем $t для переводов

const name = ref('')
const email = ref('')
const message = ref('')

const handleSubmit = () => {
  // Здесь можно обработать отправку формы (например, отправка на email или через API)
  console.log('Форма отправлена:', { name: name.value, email: email.value, message: message.value })

  // Очистка формы
  name.value = ''
  email.value = ''
  message.value = ''
}
</script>

<template>
  <footer class="bottom-bar bg-gray-900 text-white py-8">
    <div class="container mx-auto grid grid-cols-1 sm:grid-cols-2 gap-8">
      <!-- Левая часть -->
      <div class="bottom-bar-content space-y-4">
        <p class="text-center sm:text-start text-5xl">{{t('future.title')}}</p>
        <p class="text-center sm:text-start text-gray-300 text-3xl">{{t('future.description')}}</p>

        <!-- Email и соцсети -->
        <div class="space-y-2 text-start text-white">
          <a href="mailto:example@email.com" class="hover:underline font-semibold transition-all duration-300">
            example@email.com
          </a>
        </div>

        <div class="flex items-center gap-6 mt-2 text-gray-300">
          <a href="https://github.com/yourprofile" target="_blank" class="flex items-center gap-2 text-gray-300  transition-all duration-300 transform hover:scale-110">
            <i class="fab fa-github text-2xl">
              <img :src="getImageUrl('icons8-git-50.png')" :alt="github" class="w-8 h-8 object-contain" />

            </i>

            <span class="hidden sm:inline">GitHub</span>
          </a>

<!--          //#F7F7F7-->
          <a href="https://t.me/yourprofile" target="_blank" class="flex items-center gap-2 text-gray-300  transition-all duration-300 transform hover:scale-110">
            <i class="fab fa-github text-2xl">
              <img :src="getImageUrl('icons8-telegram-app-50.png')" :alt="telegram" class="w-8 h-8 object-contain" />
            </i>
            <span class="hidden sm:inline">Telegram</span>
          </a>
        </div>

      </div>

      <!-- Правая часть — контактная форма -->
      <div class="bottom-bar-content mb-8">
        <form @submit.prevent="handleSubmit" class="space-y-4">
          <input
              v-model="name"
              type="text"
              placeholder="Ваше имя"
              class="w-full p-2 bg-gray-800 text-white border border-gray-600 rounded focus:outline-none focus:ring-2 focus:ring-blue-500"
              required
          />
          <input
              v-model="email"
              type="email"
              placeholder="Ваш email"
              class="w-full p-2 bg-gray-800 text-white border border-gray-600 rounded focus:outline-none focus:ring-2 focus:ring-blue-500"
              required
          />
          <textarea
              v-model="message"
              rows="3"
              placeholder="Ваше сообщение"
              class="w-full p-2 bg-gray-800 text-white border border-gray-600 rounded resize-none focus:outline-none focus:ring-2 focus:ring-blue-500"
              required
          ></textarea>
          <button
              type="submit"
              class="bg-blue-600 hover:bg-blue-700 text-white px-4 py-2 rounded transition"
          >
            Отправить
          </button>
        </form>
      </div>
    </div>

    <!-- Нижняя строка -->
    <div class="container mx-auto mt-6 border-t border-gray-700 pt-6 text-sm text-gray-400 text-center py-6">
      <p class="mt-6"> &copy; 2025 Мое Портфолио. Все права защищены.</p>
    </div>
  </footer>
</template>
