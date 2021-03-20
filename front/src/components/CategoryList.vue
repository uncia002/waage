<template>
  <div class="list" :style="{width: reversedWidth}">
    <!-- category -->
    <div
    v-for="(Category,number) in PData"
    :key="Category.id"
    class="Categorylist"
    >
      <div class="option"  >
        <!-- :style="{'background-color': reversedColor(number)}" -->
        <p class="optioncategoryname">{{ Category.name }}</p>
        <button class="newitembotton" @click="enableCreating(Category.id)" >a</button>
      </div>
      <div class="itemlist">
        <draggable class="list-group" :list="Category.Items" group="people" @change="log">
          <div
            class="list-group-item"
            v-for="(item,index) in Category.Items"
            :key="item.name"
            :price="item.price"
            :boughtday="item.boughtday"
            :fav="item.fav"
            :overview="item.overview"
            :taglist="item.taglist"
            :alreadyhave="item.alreadyhave"
          >

          <!-- item -->
            <div v-if="detailviewActive[number][index]"
            class="item-detail"
            @click="oneClick(Category.id,index)">
              <a class="itemtitle">{{ item.name }}</a>
              <img class=itemimg src="item.img" alt="">
              <div  class="itemtext">
                <p>$:{{ item.price }}</p>
                <p>Day:{{ item.boughtday }}</p>
              </div>
              <div class="favpoc">
                <img v-if="item.fav" src="../assets/fav.png" class="icon" @click.stop="tofalse(Category.id,index)">
                <img v-else src="../assets/notfav.png" class="icon" @click.stop="totrue(Category.id,index)">
                <img v-if="item.alreadyhave" src="../assets/poc.png" class="icon" @click.stop="tofalseal(Category.id,index)">
                <img v-else src="../assets/pocket.png" class="icon" @click.stop="totrueal(Category.id,index)">
              </div>
            </div>
            <div v-else
            class="item"
            @click="oneClick(number,index)">
            <a class="itemtitle">{{ item.name }}</a>

          </div>
          </div>
        </draggable>
      </div>
    </div>

    <!-- itemEditWindow -->
    <ItemEditWindow
    v-if="editingItem.status"
    :editingItem="editingItem"
    :item="PData[editingItem.cateid].Items[editingItem.itemid]"
    :categoryname="PData[editingItem.cateid].name"
    @close="closeWindow">
    </ItemEditWindow>
    <!-- newItemWindow -->
    <NewItemEditWindow
    ref="newnameinput"
    v-if="createNewItem.status"
    :editingItem="createNewItem"
    :category="PData[createNewItem.cateid]"
    @close="closeWindow"
    @post="posted">
    </NewItemEditWindow>
  </div>
</template>

<script>
import draggable from 'vuedraggable'
import ItemEditWindow from './ItemEdit.vue'
import NewItemEditWindow from './NewItemEdit.vue'
let windowsize
export default {
  name: "two-lists",
  data () {
    return {
      editingItem:{
        status: false,
        cateid:0,
        itemid:0
      },
      createNewItem:{
        status: false,
        cateid:0
      },
      styleobject: {
        height:"35px"
      },
      result: [],
      delay: 200,
      clicks: 0,
      timer: null

    }
  },
  props: ["PData","detailviewActive"],

  components: {
    draggable,
    'ItemEditWindow':ItemEditWindow,
    'NewItemEditWindow':NewItemEditWindow
  },
  computed: {
    reversedWidth() {
      windowsize=this.PData.length*(300+2);
      console.log(windowsize)
      return windowsize+"px"
    },

  },
  methods: {
    //vuedraggable
    add: function() {
      this.list.push({ name: "Juan" });
    },
    replace: function() {
      this.list = [{ name: "Edgard" }];
    },
    clone: function(el) {
      return {
        name: el.name + " cloned"
      };
    },
    log: function(evt) {
      window.console.log(evt);
    },

    //item
    totrue: function(cat_id,index){
      this.PData[cat_id].Items[index].fav=true
    },
    tofalse: function(cat_id,index){
      this.PData[cat_id].Items[index].fav=false
    },
    totrueal(cat_id,index){
      this.PData[cat_id].Items[index].alreadyhave=true
    },
    tofalseal(cat_id,index){
      this.PData[cat_id].Items[index].alreadyhave=false
    },
    enableEditing(cateid,itemid){
      this.editingItem.status=true
      this.editingItem.cateid=cateid
      this.editingItem.itemid=itemid
      window.console.log("Editing")
    },
    enableCreating(cateid){
      this.createNewItem.status=true
      this.createNewItem.cateid=cateid
      window.console.log("createNewItem")
      this.$nextTick(function() {
        this.$refs.newnameinput.focus()
        console.log("navbarform")
      })

    },
    closeWindow(){
      this.editingItem.status=false
      this.createNewItem.status=false
      window.console.log("Closed")
    },
    posted(newitem){
      this.createNewItem.status=false
      this.PData[this.createNewItem.cateid].Items.push(newitem)
    },
    itemdetailview(number,index){
      this.$set(this.detailviewActive[number],index,!this.detailviewActive[number][index])
    },
    oneClick: function(number,index){
          this.clicks++
          if(this.clicks === 1) {
            var self = this
            this.timer = setTimeout(function() {
              self.editingItem.status=true
              self.editingItem.cateid=number
              self.editingItem.itemid=index
              self.clicks = 0
            }, this.delay);
          } else{
             clearTimeout(this.timer);
             this.clicks = 0;
             this.$set(this.detailviewActive[number],index,!this.detailviewActive[number][index])
          }
        }

  },
}
</script>

<style scoped>
::-webkit-scrollbar {
    width: 10px;
}

/*スクロールバーの軌道*/
::-webkit-scrollbar-track {
  border-radius: 10px;
  box-shadow: inset 0 0 6px rgba(0, 0, 0, .1);
}

/*スクロールバーの動く部分*/
::-webkit-scrollbar-thumb {
  background-color: rgba(0, 0, 50, .5);
  border-radius: 10px;
  box-shadow:0 0 0 1px rgba(255, 255, 255, .3);
}
.list{
  display: flex;
  flex-wrap: nowrap;
  height: 100%;
  /* background-color: #F03A47; */

}
.Categorylist{
  height: 100%;
  width: 300px;
  margin-left: 2px;
  background-color: #E8E8E8;
  border-radius: 5px;
}
.option{
  width: 300px;
  height: 40px;
  padding-top:5px;
  padding-bottom:5px;
  position:relative;
}
.optioncategoryname{
  position: absolute;
  text-align: left;
  color:black;
  font-size: 20px;
  top: 7.5px;
  left: 10px;
}
.newitembotton{
  position: absolute;
  left: 260px;
  width: 30px;
  height: 30px;
}

.itemlist{
  width: 300px;
  height: calc(100% - 40px);
  overflow-y: scroll;
  padding:0 10px;
}

.item {
  display: flex;
  width: 100%;
  height: 35px;
  background-color: white;
  margin-top: 10px;
  border-radius: 5px;
  box-shadow:2px 2px 1px rgba(0,0,0,0.1);
  position:relative;
}
.item-detail{
  display: flex;
  width: 100%;
  height: 145px;
  background-color: white;
  margin-top: 10px;
  border-radius: 5px;
  box-shadow:2px 2px 1px rgba(0,0,0,0.1);
  position:relative;
}

.itemtitle{
  font-size: 18px;
  margin-left: 10px;
  line-height: 35px;

}
.itemdetailbutton{
  position:absolute;
  left: 234px;
  top: 3px;
}

.itemdetailbuttonimg{
  width:30px;
  height:30px;
  transform: rotate(90deg);
}
.itemdetailbuttonimg-close{
  width:30px;
  height:30px;
  transform: rotate(-90deg);
}

.itemimg {
  width: 100px;
  height: 100px;
  position:absolute;
  left:10px;
  top:35px;
}

.favpoc{
  position:absolute;
  top:40px;
  left:120px;
}
.icon {
  width: 20px;
  height: 20px;
  margin-right: 10px;
}
.itemtext{
  position:absolute;
  top:70px;
  left:120px;
}
.itemtext p{
  margin-bottom: 5px;
  text-align: left;
}



</style>
