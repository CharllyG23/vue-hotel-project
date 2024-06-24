<template>
  <div class="hs-hotel-card--section-list">
    <div class="hs-hotel-card--img">
      <img :src="hotel.image" alt="hotel" />
    </div>
    <div class="hs-hotel-card--content">
      <div class="hs-hotel-card--content__name">
        <span>{{ hotel.nome }}</span>
        <hs-icon name="heart" size="sm" v-if="!isAddedToComparisonList"/>
        <hs-icon name="heart-fill" size="sm" v-else/>
        <transition name="fade">
          <div v-if="showComparisonMessage" class="comparison-popper">
            Adicionado à lista de comparação
          </div>
        </transition>
      </div>
      <span>{{ hotel.endereco }}</span>
      <span class="hs-hotel-card--content--star">
        <template v-for="n in 5" :key="n">
          <hs-icon :name="n <= hotel.avaliacao ? 'star' : 'star_border'" />
        </template>
        <strong>{{ hotel.avaliacao }}</strong>
      </span>
      <div class="hs-hotel-card--content__description">
        <span>{{ hotel.numero_quartos }}<strong> Quartos</strong></span>
        <span>{{ hotel.numero_maximo_hospedes }}<strong> Hóspedes</strong></span>
      </div>
    </div>
    <div class="hs-hotel-card--content__preco">
      <span>R$ {{ hotel.preco }}</span>
      <span class="hs-hotel-card--content__taxes">Inclui impostos e taxas</span>
      <button
        v-if="showComparisonButton"
        type="button"
        class="hs-hotel-card--content__btn-comparison"
        @click="handleComparisonClick"
        :class="{ 'selected': isSelectedHotel(hotel) }"
      >
        {{ isSelectedHotel(hotel) ? 'Selecionado' : 'Comparação de Ofertas' }}
      </button>
      <button type="button" class="hs-hotel-card--content__btn-reserve" @click="openModal(hotel)">Reserva</button>
    </div>
  </div>
</template>
<script setup lang="ts">
import { ref, onMounted } from 'vue';
import HsIcon from '@/components/HsIcon/HsIcon.vue';

interface Hotel {
  image: string;
  nome: string;
  endereco: string;
  avaliacao: number;
  numero_quartos: number;
  numero_maximo_hospedes: number;
  preco: number;
}

const props = withDefaults(defineProps<{
  hotel: Hotel;
  destino: Destino;
  showComparisonButton?: boolean;
  toggleSelectedHotel: (destino: Destino, hotel: Hotel) => void;
  isSelectedHotel: (hotel: Hotel) => boolean;
  openModal: (hotel: Hotel) => void;
}>(), {
  showComparisonButton: true
});

const isAddedToComparisonList = ref(false);
const showComparisonMessage = ref(false);

const checkIfHotelIsAdded = () => {
  const selectedHotels = JSON.parse(localStorage.getItem('selectedHotels') || '[]');
  isAddedToComparisonList.value = selectedHotels.some((selectedHotel: Hotel) => selectedHotel.nome === props.hotel.nome);
}

const handleComparisonClick = () => {
  props.toggleSelectedHotel(props.destino, props.hotel);
  isAddedToComparisonList.value = !isAddedToComparisonList.value;
  showComparisonMessage.value = isAddedToComparisonList.value;

  if (isAddedToComparisonList.value) {
    showComparisonMessage.value = true;
    setTimeout(() => {
      showComparisonMessage.value = false;
    }, 3000);
  }
}

onMounted(() => {
  checkIfHotelIsAdded();
});
</script>
<style lang="scss" scoped>
@import './HsHotelCardStyle.scss';
</style>
