/* eslint-disable */
<template>
  <div class="form">
    <p>Product url:</p>
    <input v-model="producturl" placeholder='FILL PRODUCT URl' @keypress.enter="post">
  </div>
</template>

<script>

var xhr = new XMLHttpRequest()
export default {
  data () {
    return {
      producturl: ''
    }
  },
  methods: {
    post: function () {
      console.log(this.producturl);
      xhr.open('POST', 'https://httpbin.org/post');
      xhr.setRequestHeader('content-type', 'application/x-www-form-urlencoded;charset=UTF-8');
      xhr.send(this.producturl);
      //
    }
  },
  computed: {
    validation () {
      return this.userId.length > 4 && this.userId.length < 13
    }
  }
}
</script>

<style>
.form{
  margin-left: auto;
  margin-right: auto;
  margin-bottom: 30px;
  width: 80%;
  text-align: left;
}
.form p{
  font-size: 20px;
  margin:0;
  margin-bottom: 3px;
}

.form input{
  width: 100%;
  height: 40px;
  font-size: 17px;
  padding-left: 10px;

}
</style>
