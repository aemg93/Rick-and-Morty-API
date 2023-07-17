<template>
  <div>
    <h2 class="p-3 text-white">Personajes de Rick and Morty</h2>
    <div v-if="isLoading" class="loading-animation">
      <div class="spinner"></div>
    </div>
    <div v-else-if="isError" class="error-message">
      Ha ocurrido un error al cargar los datos. Por favor, intenta nuevamente.
    </div>
    <div v-else class="container cards-ws">
      <div class="row">
        <div v-for="character in characters" :key="character.id" class="col-lg-3 col-md-6 col-sm-12">
          <div class="card col12 mb-3 bg-dark">
            <img :src="character.image" :alt="character.name" class="card-img-top">
            <div class="card-body">
              <h5 class="card-title">{{ character.name }}</h5>
              <div class="input-button-container flex-column flex-sm-row">
                <input
                    type="button"
                    :value="isSelected(character) ? 'Seleccionado' : 'Seleccionar'"
                    @click="toggleSelection(character)"
                    class="btn mb-2 mb-sm-0"
                    :class="['btn', isSelected(character) ? 'btn-success' : 'btn-secondary', isSelected(character) ? 'selected-button' : '']"
                >
                <button @click="viewSelectedDetails" class="btn btn-info">Ver detalles</button>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
    <div class="pagination d-flex justify-content-center p-5">
      <button @click="goToPreviousPage" :disabled="currentPage === 1" class="btn btn-primary btn-sm">&laquo;</button>
      <div class="page-indicator">
        <div class="page-number">{{ currentPage }}</div>
        <div class="page-number">{{ currentPage + 1 }}</div>
      </div>
      <button @click="goToNextPage" :disabled="!hasNextPage" class="btn btn-primary btn-sm">&raquo;</button>
    </div>

    <!-- Estilos para el alert -->
    <div v-if="showAlert" class="alert-container">
      <div class="alert">
        {{ alertMessage }}
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
      showAlert: false,
      alertMessage: "",
      maxCharactersSelected: 3
    };
  },

  computed: {
    ...mapGetters(['characters', 'hasNextPage', 'selectedCharacters', 'isLoading', 'isError']),
  },

  methods: {
    ...mapActions(['loadCharacters', 'toggleCharacterSelection', 'viewCharacterDetails', 'resetSelection']),
    toggleSelection(character) {
      const isSelected = this.isSelected(character);

      if (isSelected) {
        this.$store.commit('removeSelectedCharacter', character);
      } else {
        if (this.selectedCharacters.length < this.maxCharactersSelected) {
          this.$store.commit('addSelectedCharacter', character);
        } else {
          this.showAlert = true;
          this.alertMessage = "Solo se pueden seleccionar hasta tres personajes.";

          setTimeout(() => {
            this.showAlert = false;
            this.alertMessage = "";
          }, 1500);
        }
      }
    },



    isSelected(character) {
      return this.selectedCharacters.some(c => c.id === character.id);
    },
    viewSelectedDetails() {
      if (this.selectedCharacters.length === 0) {
        this.showAlert = true;
        this.alertMessage = "No has seleccionado ningún personaje.";
        return;
      }

      this.$router.push('/characterDetails');
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
.page-indicator {
  display: flex;
  align-items: center;
}

.page-number {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 40px;
  height: 40px;
  background-color: #e6e6e6;
  border: 1px solid #ccc;
  font-weight: bold;
  color: rgb(0, 0, 0);
}

.card-title {
  font-size: 16px;
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
  transform: scale(1);
  transition: transform 0.3s ease;
  color: #fff;
}

.card:hover .card-title {
  transform: scale(0.9);
}

.selected-characters .card {
  width: 200px;
  margin-right: 10px;
  display: inline-block;
}

.selected-characters .card-img-top {
  height: 200px;
  object-fit: cover;
}

.selected-characters .card-body {
  padding: 10px;
  height: 200px;
  object-fit: cover;
  display: inline-block;
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
  0% { transform: rotate(0deg); }
  100% { transform: rotate(360deg); }
}

.error-message {
  margin: 10px;
  padding: 10px;
  background-color: #dc3545;
  color: #fff;
  border-radius: 5px;
}

.input-button-container {
  display: flex;
  justify-content: space-between;
  margin-top: 8px;
}

.button-select {
  margin-right: 5px;
}

@media screen and (max-width: 1399px) {
  .button-select {
    padding: 10px 0 !important;
    font-size: 15px !important;
    width: 45%;
    margin-right: 4px;
  }
  .card-body {
    padding: 2px !important;
  }
}

.selected-button {
  padding: 4px;
}

@media screen and (max-width: 1199px) and (min-width: 992px){
  .cards-ws {
    max-width: 978px;
  }
  .btn {
    font-size: 12px;
  }
}

.alert-container {
  display: flex;
  justify-content: center;
  align-items: center;
  position: fixed;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  z-index: 9999;
}

.alert {
  background-color: #dc3545;
  color: #fff;
  padding: 10px;
  border-radius: 5px;
}
</style>
