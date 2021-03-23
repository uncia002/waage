<template>
  <div id="app">
    <Navbar :PData="PData" :detailviewActive="detailviewActive"></Navbar>
    <div class="main">
      <div class="margin">

      </div>
      <Category :PData="PData" :detailviewActive="detailviewActive"></Category>
    </div>
  </div>
</template>

<script>
import Navbar from './components/Navbar.vue'
import Category from './components/CategoryList.vue'

var PersonalData = [
  {
    id: 0,
    name: 'Gadget',
    Items: [
      {
        img: require('./assets/logo.png'),
        name: 'Apple pencil',
        price: '15000',
        boughtday: '12-1-1',
        fav: true,
        overview: "asdfghjkl",
        taglist: ["Necessities","ipad"],
        alreadyhave:false
      },
      {
        img: require('./assets/logo.png'),
        name: 'ipad',
        price: '70000',
        boughtday: '14-1-1',
        fav: false,
        overview: "asdfghjkl",
        taglist: ["Necessities","ipad"],
        alreadyhave:true
      },
      {
        img: '',
        name: 'Macbook 13inch',
        price: '130000',
        boughtday: '20-3-1',
        fav: false,
        overview: "asdfghjkl",
        taglist: ["Necessities","ipad"],
        alreadyhave:true
      },
      {
        img: '',
        name: 'Iphone 6',
        price: '70000',
        boughtday: '16-12-1',
        fav: false,
        overview: "asdfghjkl",
        taglist: ["Necessities","ipad"],
        alreadyhave:true
      },
    ]
  },
  {
    id: 1,
    name: 'Cloth',
    Items: [
      {
        img: '',
        name: 'Apple pencil',
        price: '15000',
        boughtday: '12-1-1',
        fav: false,
        overview: "detect",
        taglist: ["Necessities","ipad"],
        alreadyhave:true
      },
      {
        img: '',
        name: 'ipad',
        price: '70000',
        boughtday: '14-1-1',
        fav: false,
        overview: "asdfghjkl",
        taglist: ["Necessities","ipad"],
        alreadyhave:true
      },
      {
        img: '',
        name: 'Macbook 13inch',
        price: '130000',
        boughtday: '2022-3-1',
        fav: false,
        overview: "detect",
        taglist: ["Necessities","ipad"],
        alreadyhave:true
      },
      {
        img: '',
        name: 'Iphone 6',
        price: '70000',
        boughtday: '2216-12-1',
        fav: false,
        overview: "detect",
        taglist: ["Necessities","ipad"],
        alreadyhave:true
      },
    ]
  },
  {
    id: 2,
    name: 'Hobby',
    Items: [
      {
        img: '',
        name: 'Apple pencil',
        price: '15000',
        boughtday: '2012-1-1',
        fav: false,
        overview: "detect",
        taglist: ["Necessities","ipad"],
        alreadyhave:true
      },
      {
        img: '',
        name: 'ipad',
        price: '70000',
        boughtday: '1114-1-1',
        fav: false,
        overview: "detect",
        taglist: ["Necessities","ipad"],
        alreadyhave:true
      },
      {
        img: '',
        name: 'Macbook 13inch',
        price: '130000',
        boughtday: '1120-3-1',
        fav: false,
        overview: "detect",
        taglist: ["Necessities","ipad"],
        alreadyhave:true
      },
      {
        img: '',
        name: 'Iphone 6',
        price: '70000',
        boughtday: '1116-12-1',
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
      PData:PersonalData,
      detailviewActive:[
      ]
    }
  },
  components: {
  'Navbar': Navbar,
  'Category': Category,
  },
  mounted(){
    this.$nextTick(function(){
      let array
      for (var i=0;i<this.PData.length;i++){
        array=[]
        for (var j=0;j<this.PData[i].Items.length;j++){
          array.push(false)
        }
        this.detailviewActive.push(array)
      }
    })
    console.log(this.detailviewActive)


  },

}
</script>

<style>
html,body{
  margin: 0;
  height: 100%;
  overflow-y: hidden;
}


#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  position: relative;
  height: 100%;
  width: 100%;
}
.app::-webkit-scrollbar {
  display: none;
}
.margin{
  height: 50px;
}
.main {
  height: calc(100% - 50px);
}

</style>
