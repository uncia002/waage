<template>
<div class="filter" @click.self="closeWindow">
  <div class="item-window">
    <div class="input">
      <a>name:</a><input type="text" name="" v-model="newitem.name">
    </div>
    <div class="input">
      <a>price:</a><input type="text" name="" v-model="newitem.price">
    </div>
    <div class="input">
      <a>boughtday:</a><input type="text" name="" v-model="newitem.boughtday">
    </div>
    <div class="input">
      <a>overview:</a><input type="text" name="" v-model="newitem.overview">
    </div>

    <img v-if="newitem.fav" src="../assets/fav.png" class="fav" @click.stop="tofalse">
    <img v-else src="../assets/notfav.png" class="fav" @click.stop="totrue">
    <button type="button" class="postbutton" @click="post"></button>
    <p>already have</p>
    <input type="checkbox" name="level" v-model="newitem.alreadyhave">
    <label for="checkbox">{{ newitem.alreadyhave }}</label>
  </div>
</div>
</template>

<script>

var newitem = {
  img: null,
  name: null,
  price: null,
  boughtday: null,
  fav: false,
  overview: null,
  taglist: [null],
  alreadyhave:false
}
export default {
  data() {
    return {
      newitem:newitem
    }
  },
  props:  ["category"],
  methods: {
    totrue: function(){
      this.newitem.fav=true
    },
    tofalse: function(){
      this.newitem.fav=false
    },
    closeWindow: function(){
      window.console.log("close itemEdit")
      this.$emit('close')
    },
    post: function(){
      window.console.log("posted!!")
      this.$emit('post',this.newitem)
    }
  }
}
</script>

<style scoped>
.filter {
  position: fixed;
  width:100%;
  height: 100%;
}

.item-window {
  position: fixed;
  width:500px;
  height:500px;
  background-color:white;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  z-index:2;
  border-radius: 30px;
  border: 2px solid black;
  box-shadow: 0 10px 25px 0 rgba(0, 0, 0, .5);

}
.fav {
  width: 20px;
  height: 20px;
}
.input {

}
.postbutton {
  background-color:red;
  width:30px;
  height:30px;
}
</style>
