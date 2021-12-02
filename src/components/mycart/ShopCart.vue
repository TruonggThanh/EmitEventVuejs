<template>
  <div class="shop-cart">
      <p>Cart: {{cart.length}} items</p>
      <p>Total: {{total}} vnd</p>
      <button-empty-cart
        @btn-empty-cart="emptyCart()"
      >
          <p>Empty cart</p>
      </button-empty-cart>
  </div>
</template>

<script>
import ButtonEmptyCart from './ButtonEmptyCart.vue';

export default {
    name: 'ShopCart',
    props: ['cart', 'total'],
    components: {
        ButtonEmptyCart
    },
    methods: {
        emptyCart() {
            this.$emit('empty-cart');
        }
    }
}
</script>