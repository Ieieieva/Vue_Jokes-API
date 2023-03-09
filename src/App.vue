<script setup lang="ts">
import { RouterLink, RouterView } from 'vue-router'
import HelloWorld from './components/HelloWorld.vue'
</script>

<template>
  <header class="header">
    <nav class="navigation">
      <RouterLink 
        to="/"
        class="navlink"
      >
          Home
      </RouterLink>
      <RouterLink 
        to="/favorites" 
        class="navlink"
      >
          Favorites
      </RouterLink>
    </nav>
  </header>

  <RouterView />
</template>

<style scoped>
.navigation {
  width: 100%;
  font-size: 1.5rem;
  padding: 1em;
  display: flex;
  justify-content: center;
  gap: 20px;
}

.navlink {
  text-decoration: none;
  color: var(--vt-c-primary-accent)
}

.navigation a.router-link-exact-active {
  color: var( --vt-c-secondary-accent);
}

</style>
