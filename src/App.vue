<template>
  <div class="app-container">
    <aside class="sidebar">
      <nav>
        <img src="./assets/logo.svg" alt="Logo" class="logo">
        <ul>
          <li class="nav-item">
            <img src="./assets/icon.svg" alt="Icon" class="nav-icon">
            <span>Мой склад</span>
          </li>
        </ul>
      </nav>


      <div class="support-section">
        <div class="social-icons">
          <img src="./assets/support-icon-1.svg" alt="Support Icon 1" />
          <img src="./assets/support-icon-2.svg" alt="Support Icon 2" />
          <img src="./assets/support-icon-3.svg" alt="Support Icon 3" />
        </div>
        <p class="support-text">Поддержка программы</p>
      </div>
    </aside>
    <main class="content">
      <Header />
      <MainContent />
      <Footer />
    </main>
  </div>
</template>

<script lang="ts">
import Header from './components/Header.vue';
import MainContent from './components/MainContent.vue';
import Footer from './components/Footer.vue';

export default {
  components: {
    Header,
    MainContent,
    Footer
  }
};
</script>

<style scoped>
.app-container {
  display: flex;
  height: 100vh;
  background-color: #f8f9fd;
}

.sidebar {
  width: 250px;
  background-color: #1d2746;
  color: #fff;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: space-between;
  padding: 20px;
}

nav {
  display: flex;
  flex-direction: column;
  align-items: center;
  width: 100%;
}

.logo {
  margin-bottom: 40px;
}

ul {
  list-style-type: none;
  padding: 0;
  margin: 0;
  width: 100%;
}

.nav-item {
  display: flex;
  align-items: center;
  font-size: 18px;
  padding-left: 10px;
  justify-content: center;
}

.nav-icon {
  width: 20px;
  height: 20px;
  margin-right: 10px;
}

.support-section {
  text-align: center;
  margin-top: auto;
}

.social-icons {
  display: flex;
  justify-content: center;
  margin-bottom: 10px;
}

.social-icons img {
  width: 30px;
  height: 30px;
  margin: 0 10px;
}

.support-text {
  font-size: 14px;
  color: #b0b3c3;
}

</style>
