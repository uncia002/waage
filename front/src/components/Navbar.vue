<template>
<div class="">
  <div class="navbar">
    <h4>LOGO</h4>
    <div class="">

    </div>
  </div>
  <div class="CategoryBar">
    <draggable  v-model="this.PData" draggable=".category" class="CategoryButtons" group="category" tag="div" >
      <div v-for="category in PData" :key="category.name" class="transbutton" @click="move(category.id)">
        <a>{{category.name}}</a>
        <!-- {{ reversedTitle(category.name) }} -->
      </div>
    </draggable>
    <!-- なぜかdraggableが使えない -->
  </div>
</div>
</template>


<script>
import draggable from 'vuedraggable'
export default {
  name:"Navbar",
  components:{
    'draggable': draggable,
  },
  props: ["PData","detailviewActive"],
  data() {
    return {
      CreateCategory:{
        status:false,
        name: undefined
      },
      inputdata:undefined,
      index:"",

    }
  },
  methods:{
    newcategory(){
      if(this.CreateCategory.status==false){
        this.CreateCategory.status=true
        this.$nextTick(function() {
          navbarform.focus()
          console.log(navbarform)
        })
      }else{
        this.CreateCategory.status=false
      }
      window.console.log("new category form")
    },
    submit(categoryname){
      this.index=categoryname.slice(0,1).toUpperCase() + categoryname.slice(1)
      var newcategory={
        id: this.PData.length,
        name: this.index,
        Items: []
      }
      this.PData.push(newcategory)
      this.CreateCategory.status=false
      this.inputdata=undefined
      this.detailviewActive.push({})
    },
    move(id){
      document.body.scrollTo({
        left: (id)*302,
        top:0,
        behavior: "smooth"
      });
      window.console.log("anderson kun");
    },
  },
  mounted() {
    const navbarform = this.$refs.navbarform
  },
  computed: {
    reversedTitle: function(){
      return function (name) {
        return name.slice(0,2)
      }
    },
  },
}
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Roboto&display=swap');
.navbar {
  display: flex;
  position:fixed;
  width: 100%;
  height: 40px;
  color: white;
  background-color: #111111;
  z-index: 1;
  padding: 5px;

}
.navbar p{
  color: #c6c5b9;

}
.create{
  height:40px;
  width:40px;
  border-radius: 50%;
  border: 1px solid white;
  background-color: white;
}
.group {
  position: absolute;
  z-index: 5;
  width: 300px;
  height: 90px;
  top: 50px;
  left: 20px;
  background-color: #F03A47;
  padding-left: 5px;
  padding-right: 5px;
}
.group h4 {
  margin-left: 5px;
  margin-top: 5px;
  margin-bottom: 5px;
  text-align: left;
  color: white;

}
.search_bar{
  display: flex; /*アイコン、テキストボックスを調整する*/
  height: 50px;
  width: 100%;
  background-color: #F03A47;
}



#navbarform{
  font-size: 16px;
  width: 100%; /*flexの中で100%広げる*/
  background-color: #ddd;
  border: none; /*枠線非表示*/
  outline: none; /*フォーカス時の枠線非表示*/

  box-sizing: border-box; /*横幅の解釈をpadding, borderまでとする*/
  padding-left: 10px;
}
.CategoryBar{
  position: fixed;
  width: 100%;
  height: 30px;
  top: 40px;
  padding-top: 4px;
  padding-left: 4px;
  color: lightgrey;
  background-color: #111111;
  border-top: solid 1px #454545;

}
.CategoryButtons{
  display: flex;
}


.transbutton{
  height:18px;
  padding: 0 20px;
  border-radius: 2px;
  border-right: solid 1px #454545;

  cursor: pointer;
  font-family: 'Roboto', sans-serif;
}
.transbutton a{
  font-size: 16px;

}

</style>
