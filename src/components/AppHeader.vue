<script setup>
import { ref, computed } from 'vue';
import { useI18n } from 'vue-i18n';
import { useThemeStore } from '../store/theme';
import { setLocale } from '../i18n';
import LanguageSwitcher from './LanguageSwitcher.vue';
import ThemeSwitcher from './ThemeSwitcher.vue';

const { t } = useI18n();
const menuActive = ref(false);
const currentLanguage = ref(localStorage.getItem('locale') || 'en');

// Theme store
const themeStore = useThemeStore();

const isDarkTheme = computed(() => {
  const systemPrefersDark = window.matchMedia('(prefers-color-scheme: dark)').matches;
  return themeStore.currentTheme === 'dark' || (themeStore.currentTheme === 'system' && systemPrefersDark);
});

const toggleTheme = () => {
  const newTheme = themeStore.currentTheme === 'light' ? 'dark' : 'light';
  themeStore.setTheme(newTheme);
  document.documentElement.classList.toggle('dark', newTheme === 'dark');
};

const toggleMenu = () => {
  menuActive.value = !menuActive.value;
};

const changeLanguage = (lang) => {
  currentLanguage.value = lang;
  setLocale(lang);
};
</script>

<template>
  <header class="bg-white dark:bg-gray-900 shadow-sm">
    <div class="container mx-auto px-4">
      <nav class="flex items-center justify-between h-16">
        <div class="logo text-xl font-bold text-gray-900 dark:text-white">
          {{ t('navigation.name') }}
        </div>
       
        <button 
          class="mobile-menu-btn p-2 rounded-lg hover:bg-gray-100 dark:hover:bg-gray-800 text-gray-600 dark:text-gray-300"
          @click="toggleMenu"
        >
          <span class="text-2xl">≡</span>
        </button>
        
        <div 
          class="menu flex items-center space-x-4"
          :class="{ 'active': menuActive }"
        >
          <div class="desktop-menu flex items-center space-x-6">
            <router-link 
              class="menu-item text-gray-600 dark:text-gray-300 hover:text-gray-900 dark:hover:text-white transition-colors"
              to="/"
            >
              {{ t('navigation.home') }}
            </router-link>
            <router-link 
              class="menu-item text-gray-600 dark:text-gray-300 hover:text-gray-900 dark:hover:text-white transition-colors"
              to="/blog"
            >
              {{ t('navigation.blog') }}
            </router-link>
            <router-link 
              class="menu-item text-gray-600 dark:text-gray-300 hover:text-gray-900 dark:hover:text-white transition-colors"
              to="/pricing"
            >
              {{ t('navigation.pricing') }}
            </router-link>
            <router-link 
              class="menu-item text-gray-600 dark:text-gray-300 hover:text-gray-900 dark:hover:text-white transition-colors"
              to="/contact"
            >
              {{ t('navigation.contact') }}
            </router-link>
          </div>

          <div class="flex items-center space-x-4">
            <button 
              class="theme-toggle p-2 rounded-lg hover:bg-gray-100 dark:hover:bg-gray-800 transition-colors"
              @click="toggleTheme"
              :title="isDarkTheme ? t('theme.light_mode') : t('theme.dark_mode')"
            >
              <span class="text-xl">{{ isDarkTheme ? '☀️' : '🌙' }}</span>
            </button>

            <select 
              class="lang-switch bg-transparent border border-gray-300 dark:border-gray-600 rounded-lg px-3 py-1 text-gray-600 dark:text-gray-300 focus:outline-none focus:ring-2 focus:ring-blue-500 dark:focus:ring-blue-400"
              v-model="currentLanguage" 
              @change="changeLanguage(currentLanguage)"
            >
              <option value="uk">Українська</option>
              <option value="en">English</option>
            </select>
          </div>
        </div>
      </nav>
    </div>
  </header>
</template>

<style scoped>
/* Mobile menu styles */
@media (max-width: 768px) {
  .menu {
    position: fixed;
    top: 0;
    right: -100%;
    width: 100%;
    height: 100vh;
    background-color: white;
    padding: 1rem;
    transition: right 0.3s ease;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
  }

  .menu.active {
    right: 0;
  }

  .desktop-menu {
    flex-direction: column;
    gap: 1.5rem;
    margin-bottom: 2rem;
  }

  .menu-item {
    font-size: 1.25rem;
  }

  .theme-toggle,
  .lang-switch {
    margin: 1rem 0;
  }
}

/* Dark mode styles */
.dark .menu {
  background-color: #1a1a1a;
}

/* Animation for theme toggle */
.theme-toggle {
  transition: transform 0.3s ease;
}

.theme-toggle:hover {
  transform: scale(1.1);
}
</style>
