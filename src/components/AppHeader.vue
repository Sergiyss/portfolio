<script setup>
import { ref } from 'vue';
import { useI18n } from 'vue-i18n';
import LanguageSwitcher from './LanguageSwitcher.vue';
import ThemeSwitcher from './ThemeSwitcher.vue';
import { setLocale } from '../i18n'; // Импортируем функцию для смены языка

// Для работы с переводами
const { t } = useI18n();

// Управление состоянием мобильного меню
const menuActive = ref(false);

// Состояние текущего языка
const currentLanguage = ref(localStorage.getItem('locale') || 'en');  // Язык по умолчанию

// Функция для переключения темы
const isDarkTheme = ref(false);
const toggleTheme = () => {
  isDarkTheme.value = !isDarkTheme.value;
};

// Функция для переключения мобильного меню
const toggleMenu = () => {
  menuActive.value = !menuActive.value;
};

// Прокрутка к секции на странице
const scrollToSection = (section) => {
  document.getElementById(section).scrollIntoView({ behavior: 'smooth' });
};

// Функция для переключения языка
const changeLanguage = (lang) => {
  currentLanguage.value = lang; // Обновляем текущий язык
  setLocale(lang); // Меняем язык в i18n
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
