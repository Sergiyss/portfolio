<template>
  <div class="min-h-screen bg-gray-50 dark:bg-gray-900 py-12 px-4 sm:px-6 lg:px-8">
    <div class="max-w-3xl mx-auto">
      <div class="text-center mb-12">
        <h1 class="text-3xl font-bold text-gray-900 dark:text-white mb-4">
          {{ t('contact.title') }}
        </h1>
        <p class="text-lg text-gray-600 dark:text-gray-300">
          {{ t('contact.subtitle') }}
        </p>
      </div>

      <div class="bg-white dark:bg-gray-800 rounded-xl shadow-lg overflow-hidden">
        <div class="p-8">
          <form @submit.prevent="handleSubmit" class="space-y-6">
            <div>
              <label for="name" class="block text-sm font-medium text-gray-700 dark:text-gray-300 mb-1">
                {{ t('contact.form.name') }}
              </label>
              <input
                id="name"
                v-model="form.name"
                type="text"
                :placeholder="t('contact.form.name_placeholder')"
                class="w-full px-4 py-3 rounded-lg border border-gray-300 dark:border-gray-600 
                  bg-white dark:bg-gray-700 text-gray-900 dark:text-white
                  focus:ring-2 focus:ring-blue-500 focus:border-transparent
                  transition duration-200"
                required
              />
            </div>

            <div>
              <label for="email" class="block text-sm font-medium text-gray-700 dark:text-gray-300 mb-1">
                {{ t('contact.form.email') }}
              </label>
              <input
                id="email"
                v-model="form.email"
                type="email"
                :placeholder="t('contact.form.email_placeholder')"
                class="w-full px-4 py-3 rounded-lg border border-gray-300 dark:border-gray-600 
                  bg-white dark:bg-gray-700 text-gray-900 dark:text-white
                  focus:ring-2 focus:ring-blue-500 focus:border-transparent
                  transition duration-200"
                required
              />
            </div>

            <div>
              <label for="message" class="block text-sm font-medium text-gray-700 dark:text-gray-300 mb-1">
                {{ t('contact.form.message') }}
              </label>
              <textarea
                id="message"
                v-model="form.message"
                rows="4"
                :placeholder="t('contact.form.message_placeholder')"
                class="w-full px-4 py-3 rounded-lg border border-gray-300 dark:border-gray-600 
                  bg-white dark:bg-gray-700 text-gray-900 dark:text-white
                  focus:ring-2 focus:ring-blue-500 focus:border-transparent
                  transition duration-200 resize-none"
                required
              ></textarea>
            </div>

            <div class="flex justify-center">
              <button
                type="submit"
                class="px-6 py-3 bg-blue-600 hover:bg-blue-700 text-white font-medium rounded-lg
                  transition duration-200 transform hover:scale-105 focus:outline-none focus:ring-2
                  focus:ring-blue-500 focus:ring-offset-2 dark:focus:ring-offset-gray-800"
              >
                {{ t('contact.form.submit') }}
              </button>
            </div>
          </form>
        </div>

        <div class="bg-gray-50 dark:bg-gray-700 px-8 py-6">
          <div class="flex justify-center space-x-8">
            <a
              href="https://github.com/yourprofile"
              target="_blank"
              class="flex items-center space-x-2 text-gray-600 dark:text-gray-300
                hover:text-gray-900 dark:hover:text-white transition duration-200"
            >
              <img
                :src="getImageUrl('icons8-git-50.png')"
                :alt="t('contact.social.github')"
                class="w-6 h-6"
              />
              <span class="text-sm font-medium">{{ t('contact.social.github') }}</span>
            </a>

            <a
              href="https://t.me/yourprofile"
              target="_blank"
              class="flex items-center space-x-2 text-gray-600 dark:text-gray-300
                hover:text-gray-900 dark:hover:text-white transition duration-200"
            >
              <img
                :src="getImageUrl('icons8-telegram-app-50.png')"
                :alt="t('contact.social.telegram')"
                class="w-6 h-6"
              />
              <span class="text-sm font-medium">{{ t('contact.social.telegram') }}</span>
            </a>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';
import { useI18n } from 'vue-i18n';
import { getImageUrl } from '@/utils/helpers';

const { t } = useI18n();

const form = ref({
  name: '',
  email: '',
  message: ''
});

const handleSubmit = () => {
  // Handle form submission
  console.log('Form submitted:', form.value);
  // Reset form
  form.value = {
    name: '',
    email: '',
    message: ''
  };
};
</script>

<style scoped>
/* Add any custom styles here if needed */
</style>
  