<template>
  <div class="cartcontrol">
    <transition name="fade">
      <div v-show="food.count > 0"
           @click.stop.prevent="decreaseCart"
           class="cart-decrease">
        <transition name="rotate">
          <span v-show="food.count > 0"
                class="inner icon-remove_circle_outline"></span>
        </transition>
      </div>
    </transition>
    <div v-show="food.count > 0"
         class="cart-count">{{food.count}}</div>
    <div @click.stop.prevent="addCart"
         class="cart-add icon-add_circle"></div>
  </div>
</template>

<script>
import Vue from 'vue'
export default {
  props: {
    food: {
      type: Object
    }
  },
  methods: {
    decreaseCart(event) {
      if (!event._constructed) {
        return
      }
      if (this.food.count) {
        this.food.count--
      }
    },
    addCart(event) {
      if (!event._constructed) {
        return
      }
      if (!this.food.count) {
        Vue.set(this.food, 'count', 1)
      } else {
        this.food.count++
      }
      this.$emit('cart-add', event.target)
    }
  }
}
</script>

<style lang="stylus" scoped>
.cartcontrol
  font-size: 0
  .cart-decrease
    display: inline-block
    padding: 6px
    &.fade-enter-active, &.fade-leave-active
      transition: all 0.4s linear
    &.fade-enter, &.fade-leave-to
      opacity: 0
      transform: translate3d(24px, 0, 0)
    .inner
      display: inline-block
      line-height: 24px
      font-size: 24px
      color: rgb(0, 160, 220)
      &.rotate-enter-active, &.rotate-leave-active
        transition: all 0.4s linear
      &.rotate-enter, &.rotate-leave-to
        opacity: 0
        transform: rotate(180deg)
  .cart-count
    display: inline-block
    vertical-align: top
    width: 12px
    padding-top: 6px
    line-height: 24px
    text-align: center
    font-size: 10px
    color: rgb(147, 153, 159)
  .cart-add
    display: inline-block
    padding: 6px
    line-height: 24px
    font-size: 24px
    color: rgb(0, 160, 220)
</style>


