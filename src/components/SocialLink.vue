<template>
  <div class="footer-right px-5 px-sm-0 px-0 d-flex flex-column justify-content-center align-items-center text-center">
    <ul class="social-links m-3">
      <li v-for="(socialLink, index) in socialLinks" :key="index">
        <a
            :href="socialLink.url"
            class="social-link"
            :class="{ 'active-hover': showName && networkName === socialLink.name }"
            @mouseover="showNetworkName(socialLink.name)"
            @mouseleave="hideNetworkName()"
            target="_blank"
        >
          <i :class="socialLink.icon"></i>
        </a>
      </li>
    </ul>
    <span class="network-name" :class="{ 'show-network-name': showName }">{{ networkName }}</span>
  </div>
</template>

<script>
export default {
  data() {
    return {
      showName: false,
      networkName: '',
      socialLinks: [
        { name: 'Instagram', icon: 'bx bxl-instagram-alt', url: 'https://www.instagram.com/' },
        { name: 'Facebook', icon: 'bx bxl-facebook-square', url: 'https://www.facebook.com/profile.php?id=100094839489591' },
        { name: 'Twitter', icon: 'bx bxl-twitter', url: 'https://twitter.com/' },
        { name: 'GitHub', icon: 'bx bxl-github', url: 'https://github.com/aemg93' },
      ],
    };
  },
  methods: {
    showNetworkName(name) {
      this.networkName = name;
      this.showName = true;
    },
    hideNetworkName() {
      this.showName = false;
    },
  },
};
</script>

<style scoped>
.bx.bxl-instagram-alt,
.bx.bxl-facebook-square,
.bx.bxl-twitter,
.bx.bxl-github {
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
  color: #1B74E4;
}

.social-links li:nth-child(3) a:hover i {
  color: #00ACEE;
}

.social-links li:nth-child(4) a:hover i {
  color: #000000;
  background-color: #eef1f6;
  border: none;
  border-radius: 50%;
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

  .social-links li:nth-child(4) a i {
    color: white;
  }
}
</style>
