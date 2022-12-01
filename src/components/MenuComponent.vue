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

.tabs li{
        color: var(--red_proj);
        font-family: 'Oswald', Arial, Helvetica, sans-serif;
        font-style: italic;
        font-size: 20px;
        font-weight: bold;
        background-color: white;
        border : 0px solid var(--red_proj);
        border-radius: 0px;
        /* padding:2px 10px; */
        width: 200px;
        height: 50px;
    }
.tabs li:hover{
        background-color: var(--red_proj);
        color: white;
        border-color: white;
        cursor : pointer;
    }

.tabs a {
  align-items: center;
  display: flex;
  justify-content: center;
  border: 0px;
  color: var(--red_proj);
  margin: none;
  width:100%;
  height: 100%;
  border : 5px solid var(--red_proj);
  border-radius: 0px;
}
.tabs a:hover {
  align-items: center;
  display: flex;
  justify-content: center;
  border: 0px;
  color: white;
}
.tabs a.router-link-exact-active{
  background-color: var(--red_proj);
  color: white;
}

</style>