<template>
    <div>
        <Menu />
      <h1>Врачи</h1>
      <div class="blog-items">
        <Blog v-for="post in posts" :key="post.id" :post="post" />
      </div>
      <div v-if="isLoading">Загрузка...</div>
    </div>
  </template>
  
  <script>
  import axios from "axios";
  import Blog from "@/components/Blog.vue";
  import Menu from "@/components/Menu.vue"
  
  export default {
    components: {
      Blog,
    },
    data() {
      return {
        posts: [],
        currentPage: 1,
        totalPages: 0,
        isLoading: false,
      };
    },
    async mounted() {
      await this.fetchPosts(this.currentPage);
      window.addEventListener("scroll", this.handleScroll);
    },
    beforeDestroy() {
      window.removeEventListener("scroll", this.handleScroll);
    },
    methods: {
      async fetchPosts(page) {
        this.isLoading = true;
        try {
          const response = await axios.get(`https://vethome24.ru/wp-json/wp/v2/blog?per_page=90&page=${page}&_fields=id,title,date,featured_media`);
          this.posts.push(...response.data); // Добавляем новые посты
          const totalPosts = parseInt(response.headers["X-WP-Total"]);
          const perPage = parseInt(response.headers["X-WP-TotalPages"]);
          this.totalPages = perPage;
        } catch (error) {
          console.error("Error fetching posts:", error);
        }
        this.isLoading = false;
      },
      handleScroll() {
        if (
          window.scrollY + window.innerHeight >= document.body.offsetHeight &&
          this.currentPage < this.totalPages &&
          !this.isLoading
        ) {
          this.currentPage++;
          this.fetchPosts(this.currentPage);
        }
      },
    },
  };
  </script>
  
  <style scoped>
  .blog-items {
    display: flex;
    flex-wrap: wrap;
    gap: 20px;
    justify-content: center;
  }
  </style>