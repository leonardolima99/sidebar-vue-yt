<template>
  <aside :class="`${expanded ? 'aside--expanded' : ''}`">
    <div class="aside__logo">
      <img src="../assets/vue.svg" alt="Vue logo" />
    </div>

    <div class="menu-toggle-wrap" translate="no">
      <button class="menu-toggle" @click="ToggleMenu">
        <span class="material-icons"> keyboard_double_arrow_right </span>
      </button>
    </div>

    <h3 translate="no">Menu</h3>
    <div class="menu">
      <router-link class="menu__button" to="/">
        <span class="material-icons" translate="no">home</span>
        <span class="button__text">Home</span>
      </router-link>
      <router-link class="menu__button" to="/about">
        <span class="material-icons" translate="no">description</span>
        <span class="button__text">About</span>
      </router-link>
      <router-link class="menu__button" to="/team">
        <span class="material-icons" translate="no">group</span>
        <span class="button__text">Team</span>
      </router-link>
      <router-link class="menu__button" to="/contact">
        <span class="material-icons" translate="no">email</span>
        <span class="button__text">Contact</span>
      </router-link>
    </div>

    <div class="flex" />

    <div class="menu">
      <router-link class="menu__button" to="/settings">
        <span class="material-icons" translate="no">settings</span>
        <span class="button__text">Settings</span>
      </router-link>
    </div>
  </aside>
  <span class="blur" @click="ToggleMenu" v-if="expanded" />
</template>

<script setup>
import { ref } from "vue";

const expanded = ref(localStorage.getItem("expanded") === "true");
const ToggleMenu = () => {
  expanded.value = !expanded.value;
  localStorage.setItem("expanded", expanded.value);
};
</script>

<style lang="scss" scoped>
aside {
  display: flex;
  flex-direction: column;
  width: calc(2rem + 32px);
  overflow: hidden;
  min-height: 100vh;
  padding: 1rem;

  background-color: var(--dark);
  color: var(--light);

  transition: 0.2s ease-out;

  .flex {
    flex: 1 1 0;
  }

  .aside__logo {
    margin-bottom: 1rem;

    img {
      width: 2rem;
    }
  }

  .menu-toggle-wrap {
    display: flex;
    justify-content: flex-end;
    margin-bottom: 1rem;

    position: relative;
    top: 0;
    transition: 0.2s ease-out;

    .menu-toggle {
      .material-icons {
        font-size: 2rem;
        color: var(--light);
        transition: 0.2s ease-out;
      }

      &:hover {
        .material-icons {
          color: var(--primary);
          transform: translateX(0.5rem);
        }
      }
    }
  }

  h3,
  .menu__button .button__text {
    opacity: 0;
    transition: 0.3s ease-out;
  }

  h3 {
    color: var(--grey);
    font-size: 0.875rem;
    margin-bottom: 0.5rem;
    text-transform: uppercase;
  }

  .menu {
    margin: 0 -1rem;

    .menu__button {
      display: flex;
      align-items: center;
      text-decoration: none;

      padding: 0.5rem 1rem;
      transition: 0.2s ease-out;

      .material-icons {
        font-size: 2rem;
        color: var(--light);
        transition: 0.2s ease-out;
      }

      .button__text {
        color: var(--light);
        transition: 0.2s ease-out;
      }

      &:hover,
      &.router-link-exact-active {
        background-color: var(--dark-alt);

        .material-icons,
        .button__text {
          color: var(--primary);
        }
      }

      &.router-link-exact-active {
        border-right: 5px solid var(--primary);
      }
    }
  }

  &.aside--expanded {
    width: var(--sidebar-width);

    .menu-toggle-wrap {
      top: -3rem;

      .menu-toggle {
        transform: rotate(-180deg);
      }
    }

    h3,
    .menu__button .button__text {
      opacity: 1;
    }

    .menu__button {
      .material-icons {
        margin-right: 1rem;
      }
    }
  }

  @media (max-width: 768px) {
    position: fixed;
    z-index: 99;
  }
}

@media (max-width: 768px) {
  .blur {
    width: 100vw;
    height: 100vh;
    background-color: rgba($color: #000000, $alpha: 0.7);
    transition: 0.8s ease-out;

    position: absolute;
    top: 0;
    left: 0;
    z-index: 9;
  }
}
</style>
