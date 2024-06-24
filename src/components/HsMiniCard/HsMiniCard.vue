<template>
    <div class="hs-mini-card">
      <img :src="props.data.image" alt="Hotel Image" class="hs-mini-card--img" />
      <div class="hs-mini-card--content">
        <h2>{{ props.data.nome }}</h2>
        <p class="avaliacao">Avaliação: {{ props.data.avaliacao }}</p>
        <p class="price">Preço: R$ {{ props.data.preco }}</p>
      </div>
    </div>
  </template>
<script setup lang="ts">
  interface Data {
    nome: string;
    endereco: string;
    avaliacao: number;
    preco: number;
    numero_quartos: number;
    numero_maximo_hospedes: number;
    datas_disponiveis: string[];
    image: string;
  }

  const props = defineProps<{
    data: Data;
  }>();
</script>
<style lang="scss" scoped>
@import './HsMiniCardStyle.scss';  
</style>
