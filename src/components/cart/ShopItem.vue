<template>
    <div class="shop-item">
        <img />
        <div class="item-detail">
            <p><strong>{{item.name}}</strong></p>
            <p>Price: <strong>${{item.price}}</strong></p>
        </div>
        <button-add-cart 
            @button-clicked="addToCart(item)"
            :item="item"    
        >
            <p>Add to cart</p>
        </button-add-cart>
    </div>
</template>

<script>
import ButtonAddCart from './ButtonAddCart.vue';

export default {
    name: 'ShopItem',
    components: {ButtonAddCart},
    props: ['item'],
    data() {
        return {}
    },
    methods: {
        addToCart(item) {
            this.$emit('update-cart', item)
        }
    }
}
</script>

<style scoped>

</style>