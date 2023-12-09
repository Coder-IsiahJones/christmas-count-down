<script lang="ts" setup>
import { ref, computed, watch } from 'vue';

const daysToChristmas = ref<number>(0);
const hours = ref<number>(0);
const minutes = ref<number>(0);
const seconds = ref<number>(0);

const countdownText = computed(() => {
  // Determine the appropriate unit of time for the countdown
  return daysToChristmas.value >= 1
    ? 'Days'
    : hours.value >= 1
      ? 'Hours'
      : minutes.value >= 1
        ? 'Minutes'
        : 'Seconds';
});

const calcCountdown = () => {
  const currentDate = new Date();
  const currentYear = currentDate.getFullYear();
  let christmasDate = new Date(currentYear, 11, 25, 0, 0, 0);

  if (currentDate > christmasDate) {
    christmasDate = new Date(currentYear + 1, 11, 25);
  }

  const timeDifference = christmasDate.getTime() - currentDate.getTime();

  daysToChristmas.value = Math.floor(timeDifference / (1000 * 60 * 60 * 24));
  hours.value = Math.floor((timeDifference % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60));
  minutes.value = Math.floor((timeDifference % (1000 * 60 * 60)) / (1000 * 60));
  seconds.value = Math.floor((timeDifference % (1000 * 60)) / 1000);
};

calcCountdown();

// Update the countdown every second
setInterval(() => {
  calcCountdown();
}, 1000);

watch(daysToChristmas, calcCountdown);

const isChristmas = computed(() => {
  const today = new Date();
  const currentYear = today.getFullYear();

  // Compare today's date with December 25th of the current year
  const christmasDay = new Date(currentYear, 11, 25); // December is month 11 (0-indexed)

  return (
    today.getDate() === christmasDay.getDate() &&
    today.getMonth() === christmasDay.getMonth() &&
    today.getFullYear() === christmasDay.getFullYear()
  );
});

const christmasMessage = computed(() => {
  return isChristmas.value ? 'Merry Christmas! Enjoy the festive season.' : '';
});
</script>

<template>
  <main class="main">
    <section class="home">
      <div class="home__container container">
        <img src="/src/assets/santa.png" alt="image" class="home__img" />

        <div class="home__data">
          <div>
            <h1 v-if="!isChristmas" class="home__title">
              Last
              <div class="home__number">
                {{
                  daysToChristmas > 1
                    ? daysToChristmas
                    : hours > 0
                      ? hours
                      : minutes > 0
                        ? minutes
                        : seconds
                }}
              </div>
              <div class="home__text">{{ countdownText }}</div>
              To Receive Christmas
            </h1>

            <h1 v-else class="home__title">{{ christmasMessage }}</h1>
          </div>

          <p class="home__description">
            Share some Christmas spirit and happiness with these festive cards.
          </p>

          <a href="#" class="button">Send a Christmas Card</a>
        </div>

        <img src="/src/assets/bell.png" alt="image" class="home__bell" />
        <img src="/src/assets/star.png" alt="image" class="home__star" />

        <div class="home__blob"></div>
      </div>
    </section>
  </main>
</template>

<style scoped>
.home {
  height: 100vh;
  display: grid;
  align-items: center;
}

.home__container {
  position: relative;
  padding-block: 5.5rem 3rem;
  display: grid;
  row-gap: 6rem;
}

.home__img {
  width: 400px;
  transform: scale(1.2);
  transform-origin: top;
  justify-self: center;
}

.home__data {
  text-align: center;
}

.home__title {
  font-size: var(--biggest-font-size);
  font-weight: var(--font-bold);
  color: var(--title-color);
  margin-bottom: 1rem;
}

.home__number,
.home__text {
  display: inline-grid;
}

.home__number {
  position: relative;
}

.home__number {
  position: relative;
  place-items: center;
  margin: 0 0.5rem 0.75rem 0.5rem;
  width: 44px;
  height: 44px;
  background-color: var(--first-color-darker);
  border-radius: 50%;
  font-size: var(--h2-font-size);
  transform: translateY(-4px);
}

.home__number::after {
  content: '';
  position: absolute;
  width: 44px;
  height: 44px;
  border: 10px solid var(--first-color);
  border-radius: 50%;
  border-right-color: transparent;
  border-top-color: transparent;
  transform: rotate(45deg);
}

.home__description {
  margin-bottom: 2rem;
  color: var(--title-color);
}

.home__bell,
.home__star {
  position: absolute;
}

.home__bell {
  width: 50px;
  top: 14rem;
  right: -1.25rem;
  transform: rotate(30deg);
}

.home__star {
  width: 60px;
  top: 30rem;
  left: -3rem;
  transform: rotate(30deg);
}

.home__blob {
  position: absolute;
  width: 600px;
  height: 600px;
  background-color: var(--first-color-dark);
  border-radius: 4rem;
  transform: rotate(45deg);
  left: -23rem;
  top: 6rem;
  z-index: -1;
}
</style>
