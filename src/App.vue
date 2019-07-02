<template>
  <div id="app" class="container">
    <b-tag type="is-primary" size="is-medium">Autor: Leandro Jiménez</b-tag>
    <br/>
    <br/>
    <figure class="image is-128x128 imageLogo"> 
        <img src="http://fisicarangel.50webs.com/Imagen5.png">
        <b>Física II</b>
    </figure>
    <br>
    <router-view/>
  </div>
</template>

<script>
export default {
  name: 'App'
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
}
.imageLogo{
  margin: 0 auto;
  text-align: center;
}
</style>
