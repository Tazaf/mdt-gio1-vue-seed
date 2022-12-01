<template>
  <div id="div_menu">
    <section id="menu_bar">
      <img id="vue-icon" src="./assets/logo.svg" alt="Logo" />
      <MenuComponent v-bind:menu-list="menuList" />
    </section>
  </div>
  
  <!-- end Bulma: menu tabs -->
  <router-view /><!-- endroit ou sont indiqué les éléments qui font changer la page-->
</template>

<script>
import MenuComponent from './components/MenuComponent.vue'

export default {
  name: 'App-root',
  
  computed: {
    currentRoute() {
      return this.$route.path;
    }
  },
  components: {MenuComponent}
};
</script>

<style>
:root {
    --red_proj: rgb(193,4,53); 
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 10px;
  height: 100%;
  width: 100%;
}
#vue-icon {
  height: 60px;
}
#div_menu{
  background-image: linear-gradient(rgba(1,1,1,0.8),rgba(1,1,1,0));
  height: 80px;
}
#menu_bar{
  display: flex;
  justify-content: space-between;
  padding: 10px;
}
</style>
