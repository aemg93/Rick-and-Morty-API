<template>
  <div>
    <nav class="navbar navbar-expand-lg navbar-dark d-flex" :class="{ 'fixed-top': isFixedTop }">
      <button
          class="navbar-toggler mx-2 mx-sm-5"
          type="button"
          data-toggle="collapse"
          data-target="#navbarNav"
          aria-controls="navbarNav"
          aria-expanded="false"
          aria-label="Toggle navigation"
          @click="toggleMenu"
      >
        <i class="bx bx-menu"></i>
      </button>
      <div class="mx-3">
        <a href="/">
          <img src="../../public/rick-icon.svg" alt="rick">
        </a>
      </div>
      <div class="collapse navbar-collapse mx-5 flex-row-reverse" :class="{ 'show': isMenuOpen }">
        <ul class="navbar-nav ml-auto text-start justify-content-center text-center">
          <li :class="{ 'nav-item': true, 'active': $route.path === '/characterList' }">
            <router-link class="nav-link" to="/characterList" @click.native="closeMenu">Lista de personajes</router-link>
          </li>
          <li :class="{ 'nav-item': true, 'active': $route.path === '/CharacterDetails' }">
            <router-link class="nav-link" to="/CharacterDetails" @click.native="closeMenu">Detalle de personajes</router-link>
          </li>
          <li :class="{ 'nav-item': true, 'active': $route.path === '/CharacterFilter' }">
            <router-link class="nav-link" to="/CharacterFilter" @click.native="closeMenu">Categorías</router-link>
          </li>
          <li class="nav-item" v-if="hasSelectedCharacters">
            <a class="nav-link" @click.prevent="resetSelection" href="#">
              Reset
            </a>
          </li>
        </ul>
      </div>
    </nav>
    <router-view/>
  </div>
</template>

<script>
import { mapActions, mapGetters } from "vuex";

export default {
  data() {
    return {
      isMenuOpen: false,
      isFixedTop: false
    };
  },
  computed: {
    ...mapGetters(['selectedCharacters']),
    hasSelectedCharacters() {
      return this.selectedCharacters.length > 0;
    }
  },
  methods: {
    ...mapActions(['loadCharacters', 'toggleCharacterSelection', 'viewCharacterDetails', 'resetSelectedCharacters']),
    toggleMenu() {
      this.isMenuOpen = !this.isMenuOpen;
    },
    resetSelection() {
      this.resetSelectedCharacters();
      const activeNavItem = this.$el.querySelector('.nav-item.active');
      if (activeNavItem) {
        activeNavItem.classList.remove('active');
      }
    },
    handleScroll() {
      this.isFixedTop = window.scrollY > 1;
    },
    closeMenu() {
      this.isMenuOpen = false;
    }
  },
  mounted() {
    window.addEventListener('scroll', this.handleScroll);
  },
  beforeDestroy() {
    window.removeEventListener('scroll', this.handleScroll);
  }
};
</script>

<style scoped>
.nav-link {
  font-weight: bold;
  color: white;
}

.nav-link:hover {
  margin-bottom: 0;
  color: #0bf5f5;
}

.nav-link {
  font-weight: bold;
  color: white;
  position: relative;
  display: inline-block;
}

.nav-item.active .nav-link {
  color: #0bf5f5;
  border-bottom: 1px solid;
}

.navbar {
  background-color: transparent;
  backdrop-filter: blur(10px);
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.4);
}

.fixed-top {
  background-color: rgba(0, 0, 0, 0.5);
  backdrop-filter: blur(10px);
  -webkit-backdrop-filter: blur(10px);
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.4);
}

@media (max-width: 768px) {
  .navbar {
    position: fixed;
    top: 0;
    width: 100%;
    z-index: 100;
    background-color: rgba(0, 0, 0, 0.5);
    
  }

  .fixed-top {
    background-color: rgba(0, 0, 0, 0.5);
    backdrop-filter: blur(10px);
    -webkit-backdrop-filter: blur(10px);
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.4);
  }
}
</style>
