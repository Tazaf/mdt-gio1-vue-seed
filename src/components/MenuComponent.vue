<template>
  <div class="tabs is-centered">
    <ul>
      <li
        v-for="menu in menuList"
        v-bind:key="menu.name"
        v-bind:class="{ 'is-active': currentRoute === menu.route }"
      >
        <router-link :to="menu.route"> {{ menu.menuname }} </router-link>
      </li>
    </ul>
  </div>
</template>

<script>
export default{
    name : "MenuComponent",
    data() {
    return {
      menuList: [
        {
          menuname: 'Hello',
          route: '/'
        },
        {
          menuname: 'Axios',
          route: '/axios'
        },
        {
          menuname: '2d_openlayers',
          route: '/openlayers'
        },
        {
          menuname: '2d_leaflet',
          route: '/leaflet'
        },
        {
          menuname: '3d_cesium',
          route: '/cesium'
        }
      ]
    };
  }
}
</script>
<style scoped>

li{
        color: var(--red_proj);
        font-family: 'Oswald', Arial, Helvetica, sans-serif;
        font-style: italic;
        font-size: 25px;
        font-weight: bold;
        background-color: white;
        border : 5px solid var(--red_proj);
        border-radius: 10px;
        padding:2px 10px;
    }
li:hover{
        background-color: var(--red_proj);
        color: white;
        border-color: white;
        cursor : pointer;
    }

a {
  align-items: center;
  border-bottom-color: #dbdbdb;
  border-bottom-style: none;
  border-bottom-width: 0px;
  color: #4a4a4a;
  display: flex;
  justify-content: center;
  margin-bottom: -1px;
  padding: 0.5em 1em;
}
</style>