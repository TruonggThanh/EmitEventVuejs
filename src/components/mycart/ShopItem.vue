<template>
  <div class="shop-item">
    <img class="fruit-imgage" :src="item.imageSrc" :alt="item.name"/>
    <div class="item-detail">
        <p><strong>{{item.name}}</strong></p>
        <p>Price: <strong>{{item.price}}</strong>vnd</p>
    </div>
    <button-add-cart
        class="button-add-cart"
        @btn-add-cart="updateCart(item)"
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
    props: ['item'],
    components: {
        ButtonAddCart,
    },
    methods: {
        updateCart(item) {
            this.$emit('update-cart', item)
        }
    }
}
</script>

<style scoped>
.shop-item {
    display: flex;
    justify-content: space-between;
    margin-bottom: 20px;
}
.item-detail {
    margin: auto;
}
.button-add-cart {
    margin: auto;
}
.fruit-imgage {
    height: 150px;
    width: 150px;
}
</style>