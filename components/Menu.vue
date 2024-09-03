<template>
    <ul class="menu">
        <li>
            <router-link to="/">Главная</router-link>

        </li>
        <li>
            <router-link to="/doctors">Врачи</router-link>

        </li>
        <li>
            <router-link to="/blog">Блог</router-link>

        </li>
    </ul>
  </template>
  
  <script>

  </script>
  
  <style scoped>
  .menu{
    list-style: none;
    
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 30px;
    font-size: 20px;
  }
  .menu a{
    text-decoration: none;
    color: #000;
  }
  </style>