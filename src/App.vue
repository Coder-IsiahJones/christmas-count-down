<script setup lang="ts">
import SimpleHeader from './components/SimpleHeader.vue';
import HomeSection from './components/HomeSection.vue';
import SimpleModal from './components/SimpleModal.vue';
import { ref } from 'vue';

const isModalOpened = ref(false);

const openModal = () => {
  isModalOpened.value = true;
  generateChristmasCard();
};

const closeModal = () => {
  isModalOpened.value = false;
};

const christmasCard = ref('');

const generateChristmasCard = () => {
  // grab a random number between 1 and 19
  const random = Math.floor(Math.random() * 18) + 1;
  // set the image path
  christmasCard.value = `/cards/${random}.png`;

  return christmasCard.value;
};
</script>

<template>
  <SimpleHeader @openModal="openModal" />

  <HomeSection @openModal="openModal" />

  <SimpleModal :isOpen="isModalOpened" @modal-close="closeModal" name="modal">
    <template #header>AI Generated Christmas Card</template>
    <template #content>
      <img :src="christmasCard" alt="ai generate christmas card" />
    </template>
    <template #footer>
      <div class="button__group">
        <a class="button button__dark" @click="generateChristmasCard">New Card</a>
        <a class="button" @click="closeModal">Close</a>
      </div>
    </template>
  </SimpleModal>
</template>

<style scoped>
img {
  max-width: 100%;
  max-height: 100%;
  border-radius: 0.325rem;
}

.button__group {
  display: flex;
  text-align: center;
  gap: 1rem;
}

.button__group a {
  min-width: 147px;
}

@media screen and (max-width: 768px) {
  .button__group {
    flex-direction: column;
  }
}
</style>
