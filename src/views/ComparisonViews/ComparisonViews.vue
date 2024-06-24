<template>
  <div class="comparison">
    <h1 class="comparison--title">Comparação de hotéis</h1>
    <div v-if="selectedHotels.length === 0" class="comparison--no-hotels-message">
      <p>Nenhum hotel selecionado para comparação.</p>
    </div>
    <div v-else class="comparison--hotel-grid">
      <hs-hotel-card
        v-for="hotel in selectedHotels"
        :key="hotel.nome"
        :hotel="hotel"
        :destino="null"
        :showComparisonButton="false"
        :toggleSelectedHotel="toggleSelectedHotel"
        :isSelectedHotel="isSelectedHotel"
        :openModal="openModal"
      />
    </div>
  </div>
</template>
<script lang="ts" setup>
import { ref, onMounted } from 'vue';
import HsHotelCard from '@/components/HsHotelCard/HsHotelCard.vue';

const selectedHotels = ref([]);

const toggleSelectedHotel = () => {};
const isSelectedHotel = (hotel: Hotel) => {
  return selectedHotels.value.some((selectedHotel: Hotel) => selectedHotel.nome === hotel.nome);
};
const openModal = () => {};

onMounted(() => {
  const hotels = localStorage.getItem('selectedHotels');
  if (hotels) {
    selectedHotels.value = JSON.parse(hotels);
  }
});
</script>
<style lang="scss" scoped>
@import "./ComparisonViewsStyle.scss";
</style>
