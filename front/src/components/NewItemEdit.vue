<template>
<div class="filter" @click.self="closeWindow">
  <div class="item-window">

    <p class="nametitle">name.</p>
    <p class="pricetitle">price.</p>
    <p class="daytitle">bought day.</p>
    <input class="nameinput" type="text" name="name" v-model="newitem.name" ref="nameinput">
    <input class="priceinput" type="text" name="price" v-model="newitem.price">
    <input class="dayinput" type="date" name="boughtday" v-model="newitem.boughtday">
    <textarea class="overview" type="text" name="OverView" v-model="newitem.overview"></textarea>
    <div class="tag-list">
      <div class="tag" v-for="(tagname, index) in newitem.taglist" :tag="newitem.taglist" :style="{'background-color': reversedColor(index),color:reversedTextColor(index)}">
        <a>{{ tagname }}</a>
        <button type="button" name="button" @click="deletetag(index)"><img class="tagdelete" src="../assets/x.svg" alt=""></button>
      </div>
      <div v-if="newtagactive"  class="tag">
        <input ref="newtag" type="text" class="newtaginput" :style="{width: reverseTagWidth}" v-model="newtagname" @keyup.enter="submit" >
      </div>
      <button type="button" name="button" @click="newtagadd"><img class="newtagbutton" src="../assets/x.svg" alt=""></button>
    </div>
    <div class="favpoc">
      <img v-if="newitem.fav" src="../assets/fav.png" class="icon" @click.stop="newitem.fav=false">
      <img v-else src="../assets/notfav.png" class="icon" @click.stop="newitem.fav=true">
      <img v-if="newitem.alreadyhave" src="../assets/poc.png" class="icon" @click.stop="newitem.alreadyhave=false">
      <img v-else src="../assets/pocket.png" class="icon" @click.stop="newitem.alreadyhave=true">
    </div>
    <button type="button" class="postbutton" @click="post">submit!</button>
  </div>
</div>
</template>

<script>
let newtagnamelength
let i
const colorList=[
  '#E71D36','#FF9F1C','#2EC4B6','#F4EDED','#464D77',
]
var newitem = {
  img: undefined,
  name: undefined,
  price:undefined,
  boughtday: undefined,
  fav: false,
  overview: undefined,
  taglist: [],
  alreadyhave:false
}
export default {
  data() {
    return {
      newitem:newitem,
      newtagactive: false,
      newtagname: "",
      detailviewActive:[]
    }
  },
  props: ["item","categoryname"],
  computed: {
    reverseTagWidth(){
      let text=`calc(${this.newtagname.length*8}px + 25px)`
      console.log(text)
      return text
    },
    reversedColor(){
      return function(number){
        i=number%5
        return colorList[i];
      }
    },
    reversedTextColor(){
      return function(number){
        i=number%5
        if(i==1||i==3){
        return "black"}
        else{
          "white"
        }
      }
    },
  },
  methods: {
    post: function(){
      window.console.log("posted!!")
      var self=this.newitem
      this.newitem={img: undefined,
        name: undefined,
        price:undefined,
        boughtday: undefined,
        fav: false,
        overview: undefined,
        taglist: [],
        alreadyhave:false}
      this.$emit('post',self)
    },
    totrueal(){
      this.newitem.alreadyhave=true
    },
    tofalseal(){
      this.newitem.alreadyhave=false
    },
    closeWindow(){
      window.console.log("close itemEdit");
      this.$emit('close');
    },
    deletetag(index){
      this.newitem.taglist.splice(index,1)
    },
    newtagadd(){
      this.newtagactive=!this.newtagactive
      if(this.newtagactive){
        this.$nextTick(function() {
          this.$refs.newtag.focus()
          console.log("focused")
        })
      }
    },
    submit() {
      this.newtagactive=false
      this.newitem.taglist.push(this.newtagname)
      this.newtagname=""

    },
    focus: function () {
      this.$refs.nameinput.focus()
    }

  }
}
</script>

<style scoped>
.postbutton {
  background-color: white;
  width:90px;
  height:30px;
  position:absolute;
  top:385px;
  left:370px;
  color:#F03A47;
  border:solid 1px #F03A47;

}
.postbutton:hover{
  background-color: #F03A47;
  color:white;

}






:focus{
  outline: none;
}
.filter {
  position: fixed;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.6);
}
.item-window {
  position: fixed;
  width:500px;
  height:440px;
  background-color:white;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  z-index:2;
  border-radius: 10px;
  border: 2px solid black;
  box-shadow: 10px 10px 10px rgba(0,0,0,0.6);
}
.icon {
  width: 20px;
  height: 20px;
  margin-right: 10px;
}
.favpoc{
  position: absolute;
  top: 30px;
  left: 400px;
}
.nametitle{
  position: absolute;
  left:30px;
  top: 37px;
  font-size: 12px;
}
.nameinput {
  position: absolute;
  left:70px;
  top: 20px;
  font-size: 30px;
  font-weight: bold;
  overflow: hidden;
  width: 320px;
  transition: 1s;
}
.nameinput:focus, .priceinput:focus, .dayinput:focus{
  border-bottom: 1px solid #F03A47;
	background-color: transparent;
}
.pricetitle{
  position: absolute;
  left:30px;
  top: 80px;
  font-size: 12px;
}
.priceinput{
  position: absolute;
  left:70px;
  top: 68px;
  font-size: 25px;
  width: 100px;
}



.daytitle{
  position: absolute;
  left:200px;
  top: 80px;
  font-size: 12px;
}
.dayinput{
  position: absolute;
  left:290px;
  top: 70px;
  font-size: 20px;
}


.overview{
  position: absolute;
  left: 30px;
  top: 270px;
  width: 430px;
  height: 100px;
  background-color: #E0E0E0;
  padding: 8px;
  resize: none;
}
.tag-list{
  position: absolute;
  top: 120px;
  left: 30px;
  display: flex;
  width: 430px;
  flex-wrap: wrap;
}
.tag{
  padding: 6px 9px;
  margin-right: 15px;
  margin-bottom: 7.5px;
  margin-top: 7.5px;
  border-radius: 5px;
  box-shadow: 2px 2px 5px 0 rgba(0, 0, 0, .5);
  color: white;
}
.tag button{
  width: 18px;
  height: 18px;
  display: table-cell;
  vertical-align: middle;
  margin-right: 3px;
  margin-left: 3px;
}

.tagdelete{
  width: 18px;
  height:18px;
}
.newtagbutton{
  width: 18px;
  height:18px;
  transform: rotate(45deg);
  margin-top: 7px;
}
.newtaginput{
  min-width: 20px;
  width: 100px;
}
.image{
  position: absolute;
  top: 170px;
}

</style>
