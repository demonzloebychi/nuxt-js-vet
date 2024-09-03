<template>
  <div>
    <h1>{{ doctor.title.rendered }}</h1>
    <div v-html="doctor.content.rendered"></div>
  </div>
</template>

<script>
import { defineComponent } from 'vue';
import axios from 'axios';

export default defineComponent({
  async asyncData({ params }) {
    try {
      const response = await axios.get(`https://vethome24.ru/wp-json/wp/v2/doctors/${params.id}`);
      return { doctor: response.data };
    } catch (error) {
      console.error("Error fetching doctor:", error);
      return { doctor: {} };
    }
  },
});
</script>