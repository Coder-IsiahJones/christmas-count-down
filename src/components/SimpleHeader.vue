<script setup lang="ts">
import { ref } from 'vue';

const navMenu = ref<HTMLElement | null>(null);

const toggle = () => {
  navMenu.value?.classList.toggle('show-menu');
};
</script>

<template>
  <header class="header">
    <nav class="nav container">
      <!-- Nav Logo -->
      <a href="#" class="nav__logo">
        <span>Merry</span>
        <span>Christmas</span>
      </a>

      <!-- Nav Menu -->
      <div ref="navMenu" class="nav__menu">
        <!-- Nav List -->
        <ul class="nav__list">
          <li class="nav__item">
            <a href="#" class="nav__link active-link" @click="toggle"> <span>01</span> Home </a>
          </li>

          <li class="nav__item">
            <a href="#" class="nav__link" @click="toggle"> <span>02</span> Card </a>
          </li>

          <li class="nav__item">
            <a href="#" class="nav__link" @click="toggle"> <span>03</span> Contact Us </a>
          </li>
        </ul>

        <!-- Nav Buttons -->
        <div class="nav__buttons">
          <div class="nav__notifications">
            <img src="/src/assets/bell.png" alt="image" class="nav__bell" />
            <div class="nav__circle">2</div>
          </div>

          <a href="#" class="button button__dark">Send a Card</a>
        </div>

        <!-- Close Button -->
        <div class="nav__close" @click="toggle">
          <i class="ri-close-line"></i>
        </div>
      </div>

      <!-- Toggle Button -->
      <div class="nav__toggle" @click="toggle">
        <i class="ri-apps-2-line"></i>
      </div>
    </nav>
  </header>
</template>

<style scoped>
.header {
  position: fixed;
  width: 100%;
  top: 0;
  left: 0;
  background-color: var(--body-color);
  z-index: var(--z-fixed);
}

.nav,
.nav__logo,
.nav__list,
.nav__buttons {
  display: flex;
}

.nav {
  position: relative;
  height: var(--header-height);
  justify-content: space-between;
  align-items: center;
}

.nav__logo {
  color: var(--title-color);
  font-weight: var(--font-bold);
  flex-direction: column;
  align-items: center;
}

.nav__logo span:nth-child(1) {
  color: var(--first-color);
  font-size: var(--h1-font-size);
  font-family: var(--second-font);
  transform: translateY(4px);
}

.nav__logo span:nth-child(2) {
  transform: translateY(-4px);
}

.nav__toggle,
.nav__close {
  display: inline-flex;
  font-size: 1.25rem;
  color: var(--title-color);
  cursor: pointer;
}

@media screen and (max-width: 1150px) {
  .nav__menu {
    position: fixed;
    top: 0;
    right: -100%;
    background: var(--gradient-color);
    width: 80%;
    height: 100%;
    box-shadow: -2px 0 12px hsla(0, 0%, 0%, 0.2);
    padding: 6rem 2rem 0;
    display: flex;
    flex-direction: column;
    row-gap: 5rem;
    transition: right 0.4s;
  }
}

.nav__list {
  flex-direction: column;
  row-gap: 2rem;
}

.nav__link {
  color: var(--text-color);
  font-weight: var(--font-bold);
  display: inline-flex;
  flex-direction: column;
  transition: color 0.4s;
}

.nav__link span {
  font-size: var(--smaller-font-size);
}

.nav__link:hover {
  color: var(--title-color);
}

.nav__buttons {
  align-items: center;
  column-gap: 1rem;
}

.nav__notifications {
  position: relative;
  background-color: var(--first-color);
  width: 50px;
  height: 50px;
  border-radius: 0.75rem;
  display: grid;
  place-items: center;
  cursor: pointer;
  transition: background-color 0.4s;
}

.nav__notifications:hover {
  background-color: var(--first-color-alt);
}

.nav__bell {
  width: 32px;
}

.nav__circle {
  width: 24px;
  height: 24px;
  background-color: hsla(0, 100%, 39%);
  color: var(--title-color);
  font-weight: var(--font-bold);
  font-size: var(--smaller-font-size);
  border-radius: 50%;
  display: grid;
  place-items: center;
  position: absolute;
  top: -6px;
  right: -6px;
}

.nav__close {
  position: absolute;
  top: 1.15rem;
  right: 1.5rem;
}

.active-link {
  color: var(--title-color);
}

.active-link span {
  color: var(--first-color);
}

/* Show menu */
.show-menu {
  right: 0;
}

/*============= Breakpoints =============*/

@media screen and (max-width: 360px) {
  .nav__buttons {
    flex-direction: column !important;
    align-items: flex-start !important;
    row-gap: 1rem;
  }
}

@media screen and (min-width: 968px) {
  .nav__menu {
    width: 50%;
  }
}

@media screen and (min-width: 1150px) {
  .nav {
    height: calc(var(--header-height) + 2rem);
  }

  .nav__toggle,
  .nav__close {
    display: none;
  }

  .nav__menu {
    width: 100%;
    display: flex;
    align-items: center;
  }

  .nav__list {
    margin-inline: auto;
    flex-direction: row;
    column-gap: 4.5rem;
  }
}
</style>
