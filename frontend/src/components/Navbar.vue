<template>
<div class="navbar">
  <img src="../assets/plus.svg" @click="newcategory">
  <div class="group" v-if="this.newCategory.status">
    <h4>New Category Item</h4>
    <label for="text2"></label>
    <div class="search_bar">
      <input id="text2" type="text" placeholder="キーワードを入力">
    </div>
  </div>
</div>
</template>

<script>
export default {
  data() {
    return {
      newCategory:{
        status:false,
        name: null
      }
    }
  },
  methods:{
    newcategory: function(){
      this.newCategory.status=true
      window.console.log("faaaawwwww")
    }
  }
}
</script>

<style scoped>
.navbar {
  position: fixed;
  width: 60px;
  height: 100%;
  background-color: white;
  border: 1px solid black;
  z-index: 5;
  padding-top: 12px;
  padding-left: 12px;
  padding-right: 12px;
}
.navbar p{
  color: #c6c5b9;
}
img{
  width:36px;
  heihgt:36px;
}
.group {
  position: absolute;
  z-index: 5;
  width: 300px;
  height: 90px;
  left: 50px;
  background-color: white;
  border: 2px solid black;
  padding-left: 5px;
  padding-right: 5px;
}
.group h4 {
  margin-left: 5px;
  margin-top: 5px;
  margin-bottom: 5px;
  text-align: left;

}
.search_bar{
  display: flex; /*アイコン、テキストボックスを調整する*/
  height: 50px;
  width: 100%;
  background-color: #ddd;
}



#text2{
    font-size: 16px;
    width: 100%; /*flexの中で100%広げる*/
    background-color: #ddd;
    border: none; /*枠線非表示*/
    outline: none; /*フォーカス時の枠線非表示*/
    box-sizing: border-box; /*横幅の解釈をpadding, borderまでとする*/
    padding-left: 10px;
}
</style>
