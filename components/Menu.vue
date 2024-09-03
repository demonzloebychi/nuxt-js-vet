<template>
    <ul class="menu">
        <li>
            <NuxtLink to="/">Главная</NuxtLink>

        </li>
        <li>
            <NuxtLink to="/doctors">Врачи</NuxtLink>

        </li>
        <li>
            <NuxtLink to="/blog">Блог</NuxtLink>

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