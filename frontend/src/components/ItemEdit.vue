<template>
<div class="filter" @click.self="closeWindow">
  <div class="item-window">
    <input type="file" name="" value="" class="image">
    <input type="text" name="name" v-model="item.name">
    <input type="number" name="price" v-model="item.price">
    <input type="text" name="boughtday" v-model="item.boughtday">
    <input type="text" name="OverView" v-model="item.overview">
    <div class="taglist" v-for="tagname in item.taglist" :tag="item.taglist">
      <p>{{ tagname }}</p>
    </div>
    <input type="text" name="" value="">
    <img v-if="item.fav" src="../assets/fav.png" class="fav" @click.stop="tofalse">
    <img v-else src="../assets/notfav.png" class="fav" @click.stop="totrue">
    <h4>{{ categoryname }}</h4>
    <p>already have</p>
    <input type="checkbox" name="level" v-model="item.alreadyhave">
    <label for="checkbox">{{ item.alreadyhave }}</label>
  </div>
</div>
</template>

<script>
export default {
  props: ["item","categoryname"],
  methods: {
    totrue: function(){
      this.item.fav=true
    },
    tofalse: function(){
      this.item.fav=false
    },
    closeWindow: function(){
      window.console.log("close itemEdit");
      this.$emit('close');
    }
  }
}
</script>

<style>
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
</style>
