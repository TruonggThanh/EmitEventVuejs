<template>
  <div class="button-empty-cart">
      <button 
        class="button"
        @click="btnEmptyCart()"
      >
          <slot></slot>
      </button>
  </div>
</template>

<script>
export default {
    name: 'ButtonEmptyCart',
    methods: {
        btnEmptyCart() {
            this.$emit('btn-empty-cart');
        }
    }
}
</script>