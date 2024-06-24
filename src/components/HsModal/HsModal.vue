<template>
  <div v-if="isVisible" class="modal-overlay" @click="closeModal">
    <div class="modal-container" @click.stop>
      <div>
        <slot name="header">
          <h3>Modal Header</h3>
        </slot>
      </div>
      <div>
        <slot name="body">
          <p>Modal Body</p>
        </slot>
      </div>
    </div>
  </div>
</template>
<script setup lang="ts">
  defineProps({
    isVisible: {
      type: Boolean,
      required: true
    }
  });
  const emits = defineEmits(['update:isVisible']);
  const closeModal = () => {
    emits('update:isVisible', false);
  }
</script>
<style scoped>
@import './HsModalStyle.scss';
</style>
