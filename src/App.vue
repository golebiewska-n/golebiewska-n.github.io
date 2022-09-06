<script setup>
import { RouterView } from 'vue-router'
import Navigation from '@/components/Navigation.vue'
</script>

<template>
  <h2>
    NATALIA GOLEBIEWSKA
  </h2>
  <div class="wrapper">
    <Navigation />

    <div class="container">
      <RouterView />
    </div>
  </div>
</template>