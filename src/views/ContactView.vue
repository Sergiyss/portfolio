<template>
  <div class="flex justify-center px-4 py-8 bg-[#f9f9f9]">
  <div class="contact-container">
      <h1 >Контактная информация</h1>
      <p>Свяжитесь с нами через форму ниже:</p>
      <!-- Пример контактной формы -->
      <div class="bottom-bar-content mb-8">
        <form @submit.prevent="handleSubmit" class="space-y-4 w-200 flex flex-col ">
          <input
              v-model="name"
              type="text"
              placeholder="Ваше имя"
              class="w-full p-2
                 bg-white text-black border border-gray-300
                 dark:bg-gray-800 dark:text-white dark:border-gray-600
                 rounded focus:outline-none focus:ring-2 focus:ring-blue-500"
              required
          />
          <input
              v-model="email"
              type="email"
              placeholder="Ваш email"
              class="w-full p-2
           bg-white text-black border border-gray-300
           dark:bg-gray-800 dark:text-white dark:border-gray-600
           rounded focus:outline-none focus:ring-2 focus:ring-blue-500"
              required
          />
          <textarea
              v-model="message"
              rows="3"
              placeholder="Ваше сообщение"
              class="w-full p-2
           bg-white text-black border border-gray-300
           dark:bg-gray-800 dark:text-white dark:border-gray-600
           rounded resize-none focus:outline-none focus:ring-2 focus:ring-blue-500"
              required
          ></textarea>
          <button
              type="submit"
              class="bg-blue-600 hover:bg-blue-700 text-white px-4 py-2 rounded transition w-1/3  m-auto"
          >
            Отправить
          </button>
        </form>
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
    </div>
  </template>
  
  <script>
  import {getImageUrl} from "@/utils/helpers.js";

  export default {
    name: 'ContactView',
    data() {
      return {
        name: '',
        email: ''
      };
    },
    methods: {
      getImageUrl,
      submitForm() {
        // Логика отправки формы
      }
    }
  };
  </script>
  
  <style scoped>
  .contact-container {
    max-width: 920px;
    width: 100%;
    background: white;
    border-radius: 12px;
    box-shadow: 0 4px 12px rgba(0,0,0,0.05);
    padding: 2rem;
  }




  /* Стили для компонента */
  form {
    margin-top: 20px;
  }
  label {
    display: block;
    margin-bottom: 5px;
  }
  input {
    margin-bottom: 10px;
    padding: 8px;
    width: 100%;
    max-width: 300px;
  }
  button {
    padding: 10px 15px;
    background-color: #4CAF50;
    color: white;
    border: none;
    cursor: pointer;
  }
  button:hover {
    background-color: #45a049;
  }
  </style>
  