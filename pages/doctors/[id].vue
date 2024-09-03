<template>
  <div>
    <Menu />
    <BackButton />
    <div v-if="doctor">
      <h1>{{ doctor.title.rendered }}</h1>
      <img v-if="featuredImage" :src="featuredImage" :alt="doctor.title.rendered" />
      <div v-html="doctor.content.rendered"></div>
    </div>
    <div v-else>Загрузка...</div>
  </div>
</template>

<script>
import axios from 'axios';
import Menu from '@/components/Menu.vue';

export default {
  components: {
    Menu,
    BackButton,
  },
  data() {
    return {
      doctor: null,
      featuredImage: null,
    };
  },
  async asyncData({ params }) {
    try {
      // Получаем данные о враче по ID
      const res = await axios.get('https://vethome24.ru/wp-json/wp/v2/doctors');
      const doctors = res.data;

      const response = await axios.get(`https://vethome24.ru/wp-json/wp/v2/doctors/${params.id}`);
      const doctor = response.data;

   

      return { doctor,  };
    } catch (error) {
      console.error('Ошибка при загрузке информации о враче:', error);
      return { doctor: null, featuredImage: null };
    }
  },
};
</script>

<style scoped>
/* Добавьте стили по необходимости */
</style>