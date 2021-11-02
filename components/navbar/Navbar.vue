<template>
  <header>
    <div class="container md mx-auto">
      <nav class="navbar">
        <ul class="flex justify-center gap-x-2">
          <li class="navbar__item">
            <NuxtLink class="navbar__link" :to="{ name: 'index' }"
              >Home</NuxtLink
            >
          </li>
          <li class="navbar__item">
            <NuxtLink class="navbar__link" :to="{ name: 'posts' }"
              >All posts</NuxtLink
            >
          </li>
        </ul>
      </nav>
    </div>
  </header>
</template>

/* nuxt-link-active */