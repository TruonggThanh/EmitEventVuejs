<template>
  <div class="container">
    <shop-cart
      :cart="cart"
      :total="total"
      @empty-cart="emptyCart()"
    >
    </shop-cart>
    <shop-item
      v-for="item in items"
      :item="item"
      :key="item.key"
      @update-cart="updateCart(item)"
    >
    </shop-item>
  </div>
</template>

<script>
import BananaImage from './assets/banana_noun_001_01109.jpg';
import OrangeImage from './assets/cay-cam-vang-my-2.jpg';
import AppleImage from './assets/apple.jpeg';

import ShopItem from './components/mycart/ShopItem.vue';
import ShopCart from './components/mycart/ShopCart.vue';

export default {
  name: 'App',
  components: {
    ShopItem,
    ShopCart
  },
  data() {
    return {
        items: [
          {
            id: 1,
            name: 'Banana',
            price: 15000,
            imageSrc: BananaImage
          },
          {
            id: 2,
            name: 'Orange',
            price: 20000,
            imageSrc: OrangeImage
          },
          {
            id: 3,
            name: 'Apple',
            price: 30000,
            imageSrc: AppleImage
          }
        ],
        cart: [],
        total: 0
    }
  },
  computed: {
    cartTotal() {
      return this.cart.map(item => item.price).reduce((total, amount) => total + amount);
    }
  },
  methods: {
    updateCart(item) {
      this.cart.push(item);
      this.total = this.cartTotal;
    },
    emptyCart() {
      this.cart = [];
      this.total = 0;
    }
  },
  created() {
    
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300;400&display=swap');

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.container {
  max-width: 500px;
  margin: 30px auto;
  overflow: auto;
  min-height: 300px;
  border: 1px solid steelblue;
  padding: 30px;
  border-radius: 5px;
  background: #07FCDE;
}


.btn {
  display: inline-block;
  background: #000;
  color: #fff;
  border: none;
  padding: 10px 20px;
  margin: 5px;
  border-radius: 5px;
  cursor: pointer;
  text-decoration: none;
  font-size: 15px;
  font-family: inherit;
}

.btn:focus {
  outline: none;
}
.btn:active {
  transform: scale(0.98);
}
.btn-block {
  display: block;
  width: 100%;
}
</style>
