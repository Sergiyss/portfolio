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
  if (themeStore.currentTheme === 'light') {
    themeStore.setTheme('dark');
  } else if (themeStore.currentTheme === 'dark') {
    themeStore.setTheme('light');
  } else {
    // Если была выбрана "system", переключим на "dark"
    themeStore.setTheme('dark');
  }
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
  <header>
    <div class="container">
      <nav>
        <div class="logo">{{ t('navigation.name') }}</div>
       
        <button class="mobile-menu-btn" @click="toggleMenu">≡</button>
        
        <!-- Меню для мобильных устройств -->
        <div class="menu" :class="{ 'active': menuActive }">
            <div class="desktop-menu">
                <router-link class="menu-item"  to="/">{{ t('navigation.home') }}</router-link>
                <router-link class="menu-item"  to="/portfolio">{{ t('navigation.portfolio') }}</router-link>
                <router-link class="menu-item"  to="/blog">{{ t('navigation.blog') }}</router-link>
                <router-link class="menu-item"  to="/pricing">{{ t('navigation.pricing') }}</router-link>
                <router-link class="menu-item"   to="/contact">{{ t('navigation.contact') }}</router-link>
            </div>



          <div class="theme-toggle" @click="toggleTheme">
            {{ isDarkTheme ? '☀️' : '🌙' }}
          </div>
          <!-- Переключатель языка -->
          <select class="lang-switch" v-model="currentLanguage" @change="changeLanguage(currentLanguage)">
            <option value="ru">Русский</option>
            <option value="uk">Українська</option>
            <option value="en">English</option>
          </select>
        </div>
      </nav>
    </div>
  </header>
</template>

<style scoped>
/* Стиль для меню и переключателя */
.lang-switch {
  margin-left: 10px;
  padding: 5px;
  border-radius: 5px;
  border: 1px solid #ccc;
}

.theme-toggle {
  margin-top: 10px;
  cursor: pointer;
}
</style>
