<template>
  <div id="app">
    <Navbar></Navbar>
    <div class="main">
      <Category></Category>
    </div>
  </div>
</template>

<script>
import Navbar from './components/Navbar.vue'
import Category from './components/CategoryList.vue'
export default {
  name: 'App',
  components: {
    'Navbar': Navbar,
    'Category': Category,
  }
}
</script>

<style>
html,body{
  margin: 0;
  height: 100%;
}

#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  position: relative;
  height: 100%;
  width: 100%;
  overflow-y: scroll;

}

.main {
  height: 100%;
  margin-left: 60px;
}

</style>
