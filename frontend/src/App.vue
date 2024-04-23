<script setup lang="ts">
import AppHeader from '@/components/AppHeader.vue'
</script>

<template>
  <app-header />
  <div class="container mx-auto flex-1 md:px-20 px-4">
    <RouterView />
  </div>
</template>
