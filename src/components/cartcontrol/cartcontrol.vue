<template>
<div class="cartcontrol">
  <transition name="move">
    <div class="cart-decrease " v-show="food.count>0" @click="decreaseCart($event)">
        <span class="icon-remove_circle_outline inner"></span>
    </div>
  </transition>
  <div class="cart-count" v-show="food.count>0">
    {{food.count}}
  </div>
  <div class="cart-add icon-add_circle" @click="addCart($event)"></div>
</div>
</template>

<script type="text/esmascript-6">
import Vue from 'vue';

export default {
  props: {
    food: {
      type: Object
    }
  },
  methods: {
    addCart(event) {
      if (!event._constructed) {
        return;
      }
      if (!this.food.count) {
        Vue.set(this.food, 'count', 1);
      } else {
        this.food.count++;
      }
      this.$parent.eventHub.$emit('cart.add',event.target);
    },
    decreaseCart(event) {
      if (!event._constructed) {
        return;
      }
      if (this.food.count) {
        this.food.count--;
      }
    }
  }
};
</script>

<style lang="stylus" rel="stylesheet/stylus">
  .cartcontrol
    font-size: 0;
    .cart-decrease
      display: inline-block;
      padding: 6px;
      transition all 0.4s;
      &.move-enter-active,&.move-leave
        transform translate3d(0,0,0);
        .inner
          transform: rotate(0);
      &.move-enter,&.move-leave-active
        opacity: 0
        transform translate3d(24px,0,0)
        .inner
          transform rotate(180deg)
      .icon-remove_circle_outline
        display: inline-block;
        font-size: 24px;
        line-height: 24px;
        color: rgb(0,160,220);
        transition all 0.4s;
    .cart-count
      display: inline-block;
      vertical-align: top;
      width: 16px;
      padding-top:6px;
      line-height: 24px;
      text-align: center;
      font-size: 10px;
      color: rgb(147,153,159);
    .cart-add
      display: inline-block;
      padding: 6px;
      font-size: 24px;
      line-height: 24px;
      color: rgb(0,160,220);

</style>
