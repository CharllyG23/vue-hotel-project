<template>
  <div class="hs-data-reservation">
    <form @submit.prevent="handleSubmit">
      <div class="hs-data-reservation--form-group">
        <label for="name">Nome completo*</label>
        <input type="text" id="name" v-model="formData.name" required />
      </div>
      <div class="hs-data-reservation--form-group">
        <label for="email">E-mail*</label>
        <input type="email" id="email" v-model="formData.email" required />
      </div>
      <div class="hs-data-reservation--form-group">
        <label for="phone">Celular*</label>
        <input type="tel" id="phone" v-model="formData.phone" required />
      </div>
      <div class="hs-data-reservation--form-group">
        <label for="cpf">CPF*</label>
        <input type="text" id="cpf" v-model="formData.cpf" required />
      </div>
      <div class="hs-data-reservation--form-group">
        <label for="date">Data da Reserva*</label>
        <select id="date" v-model="formData.date" required>
          <option v-for="(date, index) in props.data" :key="index" :value="date">
            {{ date }}
          </option>
        </select>
      </div>
      <button type="submit" class="hs-data-reservation--btn">Reserva</button>
    </form>
  </div>
</template>
<script setup lang="ts">
import { ref } from 'vue';

interface DatesReservation {
    data: string[];
  }

  const props = defineProps<{
    data: DatesReservation;
  }>();

interface FormData {
  name: string;
  email: string;
  phone: string;
  cpf: string;
  date: string;
}

const availableDates = ref([
  '2024-07-01',
  '2024-07-02',
  '2024-07-03',
]);

const formData = ref<FormData>({
  name: '',
  email: '',
  phone: '',
  cpf: '',
  date: ''
});

const emit = defineEmits(['reservation-success']);

const handleSubmit = () => {
  console.log('Reserva realizada:', formData.value);
  alert('Reserva realizada com sucesso!');
  emit('reservation-success');
}
</script>
<style scoped>
@import './HsDataReservationStyle.scss';
</style>
