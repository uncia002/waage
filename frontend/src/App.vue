<template>
  <div id="app">
    <Navbar :PData="PData"></Navbar>
    <div class="main">
      <Category :PData="PData"></Category>
    </div>
  </div>
</template>

<script>
import Navbar from './components/Navbar.vue'
import Category from './components/CategoryList.vue'

var PersonalData = [
  {
    id: 0,
    name: 'gadget',
    Items: [
      {
        img: require('./assets/logo.png'),
        name: 'Apple pencil',
        price: '15000',
        boughtday: '12/1/1',
        fav: true,
        overview: "asdfghjkl",
        taglist: ["Necessities","ipad"],
        alreadyhave:false
      },
      {
        img: require('./assets/logo.png'),
        name: 'ipad',
        price: '70000',
        boughtday: '14/7/1',
        fav: false,
        overview: "asdfghjkl",
        taglist: ["Necessities","ipad"],
        alreadyhave:true
      },
      {
        img: '',
        name: 'Macbook 13inch',
        price: '130000',
        boughtday: '20/4/1',
        fav: false,
        overview: "asdfghjkl",
        taglist: ["Necessities","ipad"],
        alreadyhave:true
      },
      {
        img: '',
        name: 'Iphone 6',
        price: '70000',
        boughtday: '16/12/1',
        fav: false,
        overview: "asdfghjkl",
        taglist: ["Necessities","ipad"],
        alreadyhave:true
      },
    ]
  },
  {
    id: 1,
    name: 'cloath',
    Items: [
      {
        img: '',
        name: 'Apple pencil',
        price: '15000',
        boughtday: '12/1/1',
        fav: false,
        overview: "detect",
        taglist: ["Necessities","ipad"],
        alreadyhave:true
      },
      {
        img: '',
        name: 'ipad',
        price: '70000',
        boughtday: '14/7/1',
        fav: false,
        overview: "asdfghjkl",
        taglist: ["Necessities","ipad"],
        alreadyhave:true
      },
      {
        img: '',
        name: 'Macbook 13inch',
        price: '130000',
        boughtday: '20/4/1',
        fav: false,
        overview: "detect",
        taglist: ["Necessities","ipad"],
        alreadyhave:true
      },
      {
        img: '',
        name: 'Iphone 6',
        price: '70000',
        boughtday: '16/12/1',
        fav: false,
        overview: "detect",
        taglist: ["Necessities","ipad"],
        alreadyhave:true
      },
    ]
  },
  {
    id: 2,
    name: 'hobby',
    Items: [
      {
        img: '',
        name: 'Apple pencil',
        price: '15000',
        boughtday: '12/1/1',
        fav: false,
        overview: "detect",
        taglist: ["Necessities","ipad"],
        alreadyhave:true
      },
      {
        img: '',
        name: 'ipad',
        price: '70000',
        boughtday: '14/7/1',
        fav: false,
        overview: "detect",
        taglist: ["Necessities","ipad"],
        alreadyhave:true
      },
      {
        img: '',
        name: 'Macbook 13inch',
        price: '130000',
        boughtday: '20/4/1',
        fav: false,
        overview: "detect",
        taglist: ["Necessities","ipad"],
        alreadyhave:true
      },
      {
        img: '',
        name: 'Iphone 6',
        price: '70000',
        boughtday: '16/12/1',
        fav: false,
        overview: "detect",
        taglist: ["Necessities","ipad"],
        alreadyhave:true
      },
    ]
  }
]
export default {
  name: 'App',
  data(){
    return{
      PData:PersonalData
    }
  },
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
