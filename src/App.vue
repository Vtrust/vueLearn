<template>
<div>
  <v-header :seller="seller"></v-header>
  <div class="tab">
    <div class="tab-item border-1px">
      <router-link to="/goods">商品</router-link>
    </div>
    <div class="tab-item">
      <router-link to="/ratings">评论</router-link>
    </div>
    <div class="tab-item">
      <router-link to="/seller">商家</router-link>
    </div>
  </div>
  <router-view :seller="seller"></router-view>
</div>
</template>

<script type="text/esmascript-6">
import header from '@/components/header/header.vue';

const ERR_OK = 0;

export default {
  data() {
    return {
      seller: {}
    };
  },
  created() {
    this.$http.get('/api/seller').then((response) => {
      response = response.body;
      if (response.errno === ERR_OK) {// 通过变量命名来实现
        this.seller=response.data;
      }
    });
  },
  components: {
    'v-header': header
  }
};
</script>

<style lang="stylus" rel="stylesheet/stylus">
  @import "./common/stylus/mixin.styl"
  .tab
    display:flex
    width:100%
    height:40px
    line-height:40px

    .tab-item
      flex:1
      text-align:center
      & > a
        display:block
        font-size: 14px
        color: rgb(77,85,93)
        border-1px(rgba(7,17,27,0.1))
        &.active
          color:rgb(240,20,20)
</style>
