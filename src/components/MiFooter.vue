<template>
  <footer class="footer d-flex flex-column flex-sm-row justify-content-between align-items-center bg-black px-5 py-3">
    <div class="footer-left">
      <img src="https://svgdogs.com/wp-content/uploads/2021/05/anh-nen-291.jpg" alt="Logo" class="logo">
      <span class="company-name">Rick and Morty</span>
    </div>
    <div>
      <social-link />
    </div>
  </footer>
</template>


<script>
import SocialLink from "@/components/SocialLink.vue";
export default {
  components: {
    SocialLink
  }
};
</script>

<style scoped>
.footer-left {
  display: flex;
  align-items: center;
}

.logo {
  height: 30px;
  margin-right: 10px;
}

.company-name {
  font-size: 18px;
  font-weight: bold;
  color: white;
}

.bx.bxl-instagram-alt,
.bx.bxl-facebook-square,
.bx.bxl-twitter {
  font-size: 30px;
}

.social-links {
  list-style: none;
  display: flex;
  gap: 10px;
  padding: 0;
}

.social-links li a {
  color: white;
  font-size: 20px;
}

.social-links li:nth-child(1) a:hover i {
  background: radial-gradient(circle at 30% 107%, #fdf497 0%, #fdf497 5%, #fd5949 45%, #d6249f 60%, #285AEB 90%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  box-shadow: 0px 3px 10px rgba(0,0,0,.25);
}

.social-links li:nth-child(2) a:hover i {
  color: #0d46be;
}

.social-links li:nth-child(3) a:hover i {
  color: #00ACEE;
}

.network-name {
  font-size: 14px;
  font-weight: bold;
  color: white;
  margin-top: 5px;
  opacity: 0;
  transition: opacity 0.3s ease;
}

.show-network-name {
  opacity: 1;
}
@media screen and (max-width: 991px) {
  .social-links li:nth-child(1) a i {
    background: radial-gradient(circle at 30% 107%, #fdf497 0%, #fdf497 5%, #fd5949 45%, #d6249f 60%, #285AEB 90%);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    box-shadow: 0px 3px 10px rgba(0, 0, 0, .25);
  }

  .social-links li:nth-child(2) a i {
    color: #0d46be;
  }

  .social-links li:nth-child(3) a i {
    color: #00ACEE;
  }
}
</style>
