<template>
    <div class="hs-city-select">
      <label for="city">Destino</label>
      <select v-model="destination" id="city" required>
        <option value="" disabled>Para onde?</option>
        <option v-for="city in cityList" :key="city.id" :value="city.cidade">
          {{ city.cidade }}
        </option>
      </select>
    </div>
  </template>
  <script lang="ts" setup>
  import { ref, watch } from 'vue';
  import { cityList } from '@/api/mock-hotel';

  const emit = defineEmits(['update:modelValue']);

  const props = defineProps({
    modelValue: String
  });

  const destination = ref(props.modelValue);

  watch(destination, (newVal) => {
    emit('update:modelValue', newVal);
  });
  </script>
  <style lang="scss" scoped>
  @import './HsCitySelectStyle.scss';
  </style>
