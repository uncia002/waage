<template>
<div class="navbar">
  <img src="../assets/plus.svg" @click="">
  <div
  class="name"
  v-if="this.status"
  >

  </div>
</div>
</template>

<script>
export default {
  data() {
    return {
      status:false
    }
  },
  methods:{
    newcategory: function(){
      this.status=true
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
</style>
