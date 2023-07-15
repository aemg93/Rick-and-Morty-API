<template>
  <div class="container">
    <h2 class="mt-5 pt-5 text-white">Filtrar por Género:</h2>

    <div>
      <div class="row justify-content-center flex-column align-content-around">
        <div class="container mt-5 mb-5">

          <div class="d-flex align-items-center justify-content-around mb-3">
            <button
                v-for="option in genderOptions"
                :key="option.value"
                :class="['btn', 'btn-primary', { 'btn-active': selectedGender === option.value, 'btn-blue': option.value === 'Male', 'btn-pink': option.value === 'Female', 'btn-gray': option.value === '', 'btn-black': option.value === 'unknown' }]"
                @click="selectGender(option.value)"
            >
              <i :class="option.icon" class="icon"></i>
            </button>


          </div>
          <div class="card-list">
            <div v-for="character in filteredCharacters" :key="character.id" :class="['card', {'w-85': windowWidth < 463}]">
              <img :src="character.image" :alt="character.name" class="card-img-top character-image">
              <div class="card-body">
                <h4 class="card-title">{{ character.gender }}</h4>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { mapGetters, mapActions } from 'vuex';

export default {
  data() {
    return {
      selectedGender: '',
      genderOptions: [
        { value: '', icon: 'bx bxs-group' },
        { value: 'Male', icon: 'bx bx-male' },
        { value: 'Female', icon: 'bx bx-female' },
        { value: 'unknown', icon: 'bx bx-question-mark' }
      ],
      windowWidth: 0
    };
  },
  computed: {
    ...mapGetters(['characters']),
    filteredCharacters() {
      if (this.selectedGender) {
        return this.characters.filter(character => character.gender === this.selectedGender);
      } else {
        return this.characters;
      }
    },
  },
  methods: {
    ...mapActions(['loadCharacters']),
    selectGender(gender) {
      this.selectedGender = gender;
    },
    applyFilter() {
      this.loadCharacters();
    },
    handleResize() {
      this.windowWidth = window.innerWidth;
    }
  },
  created() {
    this.loadCharacters();
    window.addEventListener('resize', this.handleResize);
    this.handleResize();
  },
  destroyed() {
    window.removeEventListener('resize', this.handleResize);
  },
};
</script>

<style scoped>
.container {
  max-width: 1200px;
  margin: 0 auto;
}

.character-image {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.button-group {
  display: flex;
  margin-bottom: 10px;
}

.button-group button {
  margin-right: 10px;
}

.button-group button.active {
  background-color: #0bf5f5;
}

.button-group button.female {
  background-color: rgba(255, 105, 180, 0.3);
}

.button-group button.female.active {
  background-color: #ff69b4;
}

.icon {
  font-size: 25px;
}

.card-list {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
}

.card {
  width: 200px;
  margin: 10px;
  text-align: center;
}

.w-85 {
  width: 85%;
}

.character-image {
  width: 100%;
  height: auto;
  border-radius: 8px;
}


.btn-blue.btn-active {
  background-color: blue;
}

.btn-pink.btn-active {
  background-color: rgb(255, 156, 188);
}

.btn-gray.btn-active {
  background-color: gray;
}

.btn-black.btn-active {
  background-color: black;
}

</style>
