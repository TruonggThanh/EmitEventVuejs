<template>
    <div class="shop-cart">
        <p>Cart: {{this.cart.length}} items</p>

        <button-empty-cart @emit-empty-cart="emitEmptyCart()">
            <p>Empty cart</p>
        </button-empty-cart>

        <p>Total: ${{this.total}}</p>
    </div>
</template>

<script>
import ButtonEmptyCart from './ButtonEmptyCart.vue';

export default {
    name: 'ShopCart',
    components: {ButtonEmptyCart},
    props: ['cart', 'total'],
    data() {
        return {}
    },
    methods: {
        emitEmptyCart() {
            this.$emit('empty-cart')
        }
    }
}
</script>

<style scoped>

</style>