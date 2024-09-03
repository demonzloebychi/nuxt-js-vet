<template>
    <NuxtLink :to="`/doctors/${post.id}`" class="blog-item">
      <img v-if="featuredImage" :src="featuredImage" :alt="post.title.rendered" />
      <div class="info">
        <h2>{{ post.title.rendered }}</h2>
        <div class="date">{{ formattedDate }}</div>
      </div>
    </NuxtLink>
  </template>
  
  <script>
  import { ref, computed, onMounted } from 'vue';
  import axios from 'axios';
  
  export default {
    props: {
      post: {
        type: Object,
        required: true
      }
    },
    setup(props) {
      const featuredImage = ref(null);
      const formattedDate = computed(() => {
        if (props.post.date) {
          const dateObj = new Date(props.post.date);
          return dateObj.toLocaleDateString("ru-RU", {
            year: "numeric",
            month: "long",
            day: "numeric"
          });
        }
        return '';
      });
  
      const getImage = async () => {
        if (props.post.featured_media) {
          try {
            const response = await axios.get(`https://vethome24.ru/wp-json/wp/v2/media/${props.post.featured_media}`);
            if (response.data && response.data.source_url) {
              featuredImage.value = response.data.source_url;
            }
          } catch (error) {
            console.error("Error fetching image:", error);
          }
        }
      };
  
      onMounted(() => {
        getImage();
      });
  
      return {
        featuredImage,
        formattedDate
      };
    }
  };
  </script>
  
  <style scoped>
  .blog-item {
    background-color: #d8d8d8;
    max-width: 290px;
    padding: 10px;
    border-radius: 10px;
    text-decoration: none;
    color: #000;
  }
  .blog-item img {
    max-width: 100%;
    height: auto;
  }
  
  </style>