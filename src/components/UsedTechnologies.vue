<template>
  <div class="footer-tech">
    <ul class="tech-list mx-auto text-lg-start">
      <li><h2 class="mb-4">Tecnologías</h2></li>
      <li v-for="techItem in techItems" :key="techItem.text">
        <div class="tech-item">
          <template v-if="techItem.imageUrl">
            <img :src="techItem.imageUrl" :alt="techItem.text" class="tech-image" style="width: 30px" />
            <span class="mx-2">{{ techItem.text }}</span>
          </template>
          <template v-else>
            <i :class="['bx', techItem.icon, 'icon']"></i> {{ techItem.text }}
          </template>
        </div>
      </li>
    </ul>
  </div>
</template>

<script setup>
const techItems = [
  { icon: 'bx bxl-vuejs', text: 'Vue.js 2' },
  { icon: 'bx bx-package', text: 'Boxicons' },
  { icon: 'bx bxl-bootstrap', text: 'Bootstrap' },
  { imageUrl: 'https://www.joshsloat.com/uploads/1/2/1/8/12181336/axiosicon-256_1_orig.png', text: 'Axios' }
];
</script>

<style scoped>
.tech-list {
  list-style: none;
  padding: 0;
  margin: 0;
  font-size: 22px;
}

.tech-list li {
  margin-bottom: 10px;
}

.tech-list li .icon {
  font-size: 30px;
  margin-right: 8px;
}

.tech-list li .icon.bxl-vuejs {
  color: #4FC08D;
}

.tech-list li .icon.bx-package {
  color: #DB7093;
}

.tech-list li .icon.bxl-bootstrap {
  color: #7952B3;
}

.tech-list li .icon.bx-world {
  color: #E9B32B;
}

.tech-list li .icon.bxs-data {
  color: #764ABC;
}

.footer-tech {
  display: flex;
  align-items: center;
}

.tech-item {
  display: flex;
  align-items: center;
}
</style>
