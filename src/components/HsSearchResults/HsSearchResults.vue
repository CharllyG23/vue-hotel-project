<template>
  <section class="hs-search-results">
    <div class="hs-search-results--filter-hotel">
      <h2 class="hs-search-results--title">Resultados</h2>
      <div>
        <hs-select-filter
          :options="options"
          v-model="selectedOption"
          label="Filtros"
          placeholder="Escolher"
          @on-selected="sortResults"
        />
      </div>
    </div>
    <article v-for="destino in searchStore.results" :key="destino.id_cidade">
      <span>Cidade: <strong>{{ destino.cidade }}</strong></span>
      <br />
        <div class="hs-search-results--list">
        <hs-hotel-card
          v-for="hotel in destino.hoteis"
          :key="hotel.nome"
          :hotel="hotel"
          :destino="destino"
          :toggleSelectedHotel="toggleSelectedHotel"
          :isSelectedHotel="isSelectedHotel"
          :openModal="openModal"
        />
        </div>
    </article>
    <hs-modal :isVisible="showModal" @update:isVisible="showModal = $event">
      <template #header>
        <span><strong>Reserva:</strong> {{ selectedHotel?.nome }}</span>
      </template>
      <template #body>
        <hs-mini-card :data="selectedHotel" />
        <hs-data-reservation :data="selectedHotel?.datas_disponiveis" @reservation-success="handleReservationSuccess" />
      </template>
    </hs-modal>
  </section>
</template>
<script setup lang="ts">
import { ref, watch } from 'vue';
import { useSearchStore } from '../../store/search';
import HsSelectFilter from '@/components/HsSelectFilter/HsSelectFilter.vue';
import HsMiniCard from '@/components/HsMiniCard/HsMiniCard.vue';
import HsModal from '@/components/HsModal/HsModal.vue';
import HsDataReservation from '@/components/HsDataReservation/HsDataReservation.vue';
import HsHotelCard from '@/components/HsHotelCard/HsHotelCard.vue'

const showModal = ref(false);
const selectedHotel = ref(null);
const searchStore = useSearchStore();
searchStore.fetchHotels();
const selectedOption = ref(null);
const selectedHotels = ref([]);
const showComparison = ref(false);

const handleReservationSuccess = () => {
  showModal.value = false;
};

const options = [
  { name: 'Preço (mais barato)', value: 'priceLow' },
  { name: 'Preço (mais caro)', value: 'priceHigh' },
  { name: 'Melhores avaliações', value: 'rating' },
];

watch(selectedOption, (newOption) => {
  if (newOption) {
    sortResults(newOption.value);
  }
});

const sortResults = (option) => {
  switch (option) {
    case 'priceLow':
      searchStore.results.forEach((destino) => {
        destino.hoteis.sort((a, b) => a.preco - b.preco);
      });
      break;
    case 'priceHigh':
      searchStore.results.forEach((destino) => {
        destino.hoteis.sort((a, b) => b.preco - a.preco);
      });
      break;
    case 'rating':
      searchStore.results.forEach((destino) => {
        destino.hoteis.sort((a, b) => b.avaliacao - a.avaliacao);
      });
      break;
  }
};

const toggleSelectedHotel = (destino, hotel) => {
  const index = selectedHotels.value.findIndex((h) => h.nome === hotel.nome);
  if (index === -1) {
    selectedHotels.value.push(hotel);
  } else {
    selectedHotels.value.splice(index, 1);
  }
  showComparison.value = selectedHotels.value.length > 0;
  if (showComparison.value) {
    localStorage.setItem('selectedHotels', JSON.stringify(selectedHotels.value));
  } else {
    localStorage.removeItem('selectedHotels');
  }
};

const isSelectedHotel = (hotel) => {
  return selectedHotels.value.some((h) => h.nome === hotel.nome);
}

const openModal = (hotel) => {
  selectedHotel.value = hotel;
  showModal.value = true;
}
</script>
<style lang="scss" scoped>
@import './HsSearchResultStyle.scss';
</style>
