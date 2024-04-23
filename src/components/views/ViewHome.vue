<template>
  <div id="inside_view" :style="{backgroundImage:'url(image_fond.jpg)'}">
    <div id="text_container">
      <h1>Etat de la gravière des Délices - 4 février 2022</h1>
      <p>Ce site internet permet de visualiser l'état de la gravière au 4 février 2022 grâce à une carte interactive 2D et à la modélisation 3D du terrain.</p>
      <p>Des options supplémentaires vont être ajoutés comme la possibilité de visualiser les états des années précédentes ou l'affichage des volumes des différents cubages selon les secteurs.</p>
      <p>Pour l'instant les rapports sont disponible via téléchargement au format PDF selon la liste ci-dessous :</p>
      <ul>
        <li><a href="2019-12_RAPPORT.PDF" target="_blank">Rapport de décembre 2019</a></li>
        <li><a href="2020-11_RAPPORT.PDF" target="_blank">Rapport de novembre 2020</a></li>
        <li><a href="2022-02_RAPPORT.PDF" target="_blank">Rapport de février 2022</a></li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  name: 'home',
  data() {
    
  }
};
</script>
<style scoped>
#inside_view {
  height: calc(100% - 80px);
  display: flex;
}
#text_container{
  background-color: rgb(255,255,255,0.6);
  width:800px;
  margin: auto;
  border-radius: 20px;
  padding: 5px 30px;
}
h1{
  font-size: 20px;
  font-weight: bold;
  margin: 20px 0px;
  text-shadow:  0px 0px 10px white, 0px 0px 5px white, 0px 0px 5px white;
}
p{
  margin: 10px 0px;;
  text-shadow:  0px 0px 10px white, 0px 0px 5px white, 0px 0px 5px white;
}
ul{
  list-style-type: square;
  margin: 10px 0px;
  text-shadow:  0px 0px 10px white, 0px 0px 5px white, 0px 0px 5px white;
}
</style>