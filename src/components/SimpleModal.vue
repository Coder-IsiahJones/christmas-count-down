<script lang="ts" setup>
import { defineProps, defineEmits, ref } from 'vue';
import { onClickOutside } from '@vueuse/core';

const props = defineProps({
  isOpen: Boolean,
});

const emit = defineEmits(['modal-close']);

const target = ref(null);
onClickOutside(target, () => emit('modal-close'));
</script>

<template>
  <div v-if="isOpen" class="modal-mask">
    <div class="modal-wrapper">
      <div class="modal-container" ref="target">
        <div class="modal-header">
          <slot name="header"> default header </slot>
        </div>
        <div class="modal-body">
          <slot name="content"> default content </slot>
        </div>
        <div class="modal-footer">
          <slot name="footer"> </slot>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.modal-mask {
  position: fixed;
  z-index: 9998;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  overflow-y: auto;
}

.modal-container {
  max-width: 50%;
  margin: 150px auto;
  padding: 1.25rem 1.875rem;
  background-color: #fff;
  border-radius: 0.325rem;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.33);
}

.modal-header {
  display: flex;
  justify-content: center;
  color: var(--first-color-darker);
  font-weight: var(--font-bold);
  font-size: var(--h2-font-size);
  padding-bottom: 2rem;
}

.modal-footer {
  display: flex;
  justify-content: center;
  padding-top: 1rem;
}

@media screen and (max-width: 768px) {
  .modal-header {
    text-align: center;
  }

  .modal-container {
    max-width: 90%;
    margin: 3rem auto;
  }
}
</style>
