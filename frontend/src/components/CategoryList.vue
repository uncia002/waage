<template>
  <div class="list" v-bind:style="{width: reversedWidth}">
    <!-- category -->
    <div
    v-for="Category in PData"
    v-bind:key="Category.id"
    class="Categorylist">
      <div class="option">
        <p class="optioncategoryname">{{ Category.name }}</p>
        <button class="newitembotton" @click="enableCreating(Category.id)" >a</button>
      </div>
      <div class="itemlist">
        <draggable class="list-group" :list="Category.Items" group="people" @change="log">
          <div
            class="list-group-item"
            v-for="(Item,index) in Category.Items"
            :key="Item.name"
            :price="Item.price"
            :boughtday="Item.boughtday"
            :fav="Item.fav"
            :overview="Item.overview"
            :taglist="Item.taglist"
            :alreadyhave="Item.alreadyhave"
          >

          <!-- item -->
            <div
            class="item"
            :class='{colorEggBlue: !Item.alreadyhave}'
            @click="enableEditing(Category.id,index)">
              <img :src="Item.img" class="itemimg">
              <div class="text">
                <h5>{{ Item.name }}</h5>
                <p>{{ Item.price }}</p>
                <p>{{ Item.boughtday }}</p>
                <p>{{ index+1 }}</p>
              </div>
              <img v-if="Item.fav" src="../assets/fav.png" class="fav" @click.stop="tofalse(Category.id,index)">
              <img v-else src="../assets/notfav.png" class="fav" @click.stop="totrue(Category.id,index)">
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
var windowsize
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
      }
    }
  },
  props: ["PData"],
  components: {
    draggable,
    'ItemEditWindow':ItemEditWindow,
    'NewItemEditWindow':NewItemEditWindow
  },
  computed: {
    reversedWidth: function() {
      windowsize=this.PData.length*(300+2);
      console.log(windowsize)
      return windowsize+"px"
    }
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
    enableEditing: function(cateid,itemid){
      this.editingItem.status=true
      this.editingItem.cateid=cateid
      this.editingItem.itemid=itemid
      window.console.log("Editing")
    },
    enableCreating: function(cateid){
      this.createNewItem.status=true
      this.createNewItem.cateid=cateid
      window.console.log("createNewItem")
    },
    closeWindow: function(){
      this.editingItem.status=false
      this.createNewItem.status=false
      window.console.log("Closed")
    },
    posted: function(newitem){
      this.createNewItem.status=false
      this.PData[this.createNewItem.cateid].Items.push(newitem)
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
}
.Categorylist{
  height: 100%;
  width: 300px;
  background-color: #FEF7F0;
  margin-left: 2px;
}
.option{
  width: 300px;
  height: 40px;
  background-color: white;
  border: 1px solid black;
  padding-top:5px;
  padding-bottom:5px;
  position:relative;
}
.optioncategoryname{
  position: absolute;
  text-align: left;
  color:red;
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
  background-color: white;
  overflow-y: scroll;
}
.itemlist p{
  margin:0;
}
.item {
  display: flex;
  width: 100%;
  height: 110px;
  background-color: #ED6A5A;
  margin-bottom: 2px;
}


.colorEggBlue{
  background-color: #909090  ;
}

.itemimg {
  width: 100px;
  height: 100px;
  margin-left: 5px;
  margin-top: 5px;
  margin-bottom: 5px;
}


.fav {
  width: 20px;
  height: 20px;
}
</style>
