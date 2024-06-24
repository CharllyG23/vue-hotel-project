<template>
  <header class="header">
    <div class="header-logo">
      <hs-icon name="hotel" size="sm" />
      <router-link to="/">Hotel Nordico</router-link>
    </div>
    <nav class="header-nav">
      <router-link to="/comparison">
        Comparação
      </router-link>
      <a href="#" target="_blank">Dicas</a>
    </nav>
  </header>
</template>
<script setup lang="ts">
import HsIcon from '@/components/HsIcon/HsIcon.vue';

</script>
<style lang="scss" scoped>
@import './HsHeaderStyle.scss';
</style>
