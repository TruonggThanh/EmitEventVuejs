<template>
  <div class="button-add-cart">
    <button 
       class="button"
       @click="btnAddCart(item)"
    >
        <slot></slot>
    </button>
  </div>
</template>

<script>
export default {
    name: 'ButtonAddCart',
    props: ['item'],
    methods: {
        btnAddCart(item) {
            this.$emit('btn-add-cart', item)
        }
    }
}
</script>