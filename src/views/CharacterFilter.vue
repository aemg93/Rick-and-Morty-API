<template>
  <div class="container">
    <h2 class="mt-5 pt-5 text-white">Filtrar personajes por género:</h2>

    <div v-if="isLoading" class="loading-animation">
      <div class="spinner"></div>
    </div>

    <div v-else-if="isError" class="error-message">
      Ha ocurrido un error al cargar los datos. Por favor, intenta nuevamente.
    </div>

    <div v-else>
      <div class="filter-buttons d-flex justify-content-center p-3">
        <button
            v-for="gender in genders"
            :key="gender.value"
            @click="filterByGender = gender.value"
            :class="{
            'btn-primary': filterByGender === gender.value,
            'btn-secondary': filterByGender !== gender.value
          }"
            class="btn btn-sm mr-2 px-3 py-2 mx-1 mx-sm-5"
        >
          <i :class="[gender.icon, 'icon-lg']"></i>
        </button>
      </div>

      <div class="row justify-content-center">
        <div v-for="character in filteredCharacters" :key="character.id" class="col-lg-3 col-md-6 col-sm-12">
          <div class="card col12 mb-3 bg-dark">
            <div class="card-body">
              <img :src="character.image" class="card-img-top mb-3" alt="Imagen del personaje">
              <h5 class="card-title text-white">{{ character.name.split(' ')[0] }}</h5>
              <p class="card-text text-white">Género: {{ character.gender }}</p>
            </div>
          </div>
        </div>
      </div>
      <div class="pagination d-flex justify-content-center p-5">
        <button @click="goToPreviousPage" :disabled="currentPage === 1" class="btn btn-primary btn-sm">&laquo;</button>
        <div class="page-indicator d-flex align-items-center ml-3">
          <div class="page-number bg-white text-black mr-2 page-number-height">{{ currentPage }}</div>
          <div class="page-number bg-white text-black page-number-height">{{ currentPage + 1 }}</div>
        </div>
        <button @click="goToNextPage" :disabled="!hasNextPage" class="btn btn-primary btn-sm">&raquo;</button>
      </div>
    </div>
  </div>
</template>

<script>
import { mapActions, mapGetters } from 'vuex';

export default {
  data() {
    return {
      showDetails: false,
      currentPage: 1,
      filterByGender: null,
      genders: [
        { value: null, icon: 'bx bxs-group' },
        { value: 'male', icon: 'bx bx-male' },
        { value: 'female', icon: 'bx bx-female' },
        { value: 'unknown', icon: 'bx bx-question-mark' },
      ],
    };
  },

  computed: {
    ...mapGetters(['characters', 'hasNextPage', 'selectedCharacters', 'isLoading', 'isError']),
    filteredCharacters() {
      if (!this.filterByGender) {
        return this.characters;
      }

      const genderKey =
          this.filterByGender === 'female'
              ? 'Female'
              : this.filterByGender === 'male'
                  ? 'Male'
                  : this.filterByGender === 'unknown'
                      ? 'unknown'
                      : '';

      return this.characters.filter((character) => character.gender === genderKey);
    },
  },

  methods: {
    ...mapActions(['loadCharacters', 'toggleCharacterSelection', 'viewCharacterDetails', 'resetSelection']),
    toggleSelection(character) {
      this.toggleCharacterSelection(character);
    },
    isSelected(character) {
      return this.selectedCharacters.some((c) => c.id === character.id);
    },

    goToPreviousPage() {
      if (this.currentPage > 1) {
        this.loadCharacters(this.currentPage - 1);
      }
    },
    goToNextPage() {
      if (this.hasNextPage) {
        this.loadCharacters(this.currentPage + 1);
      }
    },
    loadCharacters(page) {
      this.currentPage = page;
      this.$store.dispatch('loadCharacters', page);
    },
    resetSelection() {
      this.$store.commit('resetSelectedCharacters');
    },
  },

  created() {
    this.loadCharacters(this.currentPage);
  },
};
</script>

<style scoped>
.container {
  max-width: 1200px;
  margin: 0 auto;
}

.loading-animation {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 200px;
}

.spinner {
  border: 4px solid #f3f3f3;
  border-top: 4px solid #3498db;
  border-radius: 50%;
  width: 30px;
  height: 30px;
  animation: spin 1s linear infinite;
}

@keyframes spin {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}

.error-message {
  margin: 10px;
  padding: 10px;
  background-color: #dc3545;
  color: #fff;
  border-radius: 5px;
}

.filter-buttons {
  margin-bottom: 20px;
}

.card-title,
.card-text {
  font-family: 'Roboto', sans-serif;
  color: white;
}
.page-number-height {
  height: 30px;
  width: 25px;
  display: flex;
  justify-content: center;
  align-items: center;
  border: solid 1px black;
}

.icon-lg {
  font-size: 24px;
}
@media screen and (max-width: 1399px) {

}

@media screen and (max-width: 1199px) and (min-width: 992px) {

}
</style>
