<template>
<div class="navbar">
  <div class="create" @click="newcategory"></div>
  <div v-for="category in this.PData" :id="category.id" :name="category.name" class="transbutton" @click="move(category.id)">
    <a>{{ reversedTitle(category.name) }}</a>
  </div>
  <div class="group" v-show="this.CreateCategory.status">
    <h4>New Category Item</h4>
    <label for="navbarform"></label>
    <div class="search_bar">
      <input ref="navbarform" id="navbarform" type="text" placeholder="キーワードを入力" v-model="inputdata" @keyup.enter="submit(inputdata)" >
    </div>
  </div>
</div>
</template>


<script>
export default {
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
    }
  },
}
</script>

<style scoped>
.navbar {
  display: flex;
  position:fixed;
  width: 100%;
  height: 50px;
  color: white;
  background-color: #F03A47;
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
  color:;

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
.transbutton{
  height:40px;
  width:40px;
  border-radius: 50%;
  display: table;
  text-align: center;
  margin-left: 8px;
}
.transbutton a{
  font-size: 25px;
  display: table-cell;
  vertical-align: middle;
  text-decoration: underline white;

}

</style>
