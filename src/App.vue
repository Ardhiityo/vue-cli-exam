<template>
  <div id="app" class="container mt-5">
    <router-view :cart="cart" :cartQty="cartQty" :cartSum="cartSum" :max.sync="max" :slider="slider" :products="products"
      @slider-status="sliderStatus" @delete-items="deleteItems" @add-items="addItems">
    </router-view>
  </div>
</template>

<script>

export default {
  name: "app",
  data: function () {
    return {
      products: [],
      max: 50,
      cart: [],
      slider: true
    }
  },
  mounted: function () {
    fetch("https://hplussport.com/api/products/order/price")
      .then(res => res.json())
      .then(res => this.products = res);
  },
  computed: {
    cartQty: function () {
      let sumQty = 0;
      for (const key in this.cart) {
        sumQty += this.cart[key].qty;
      }
      return sumQty;
    },
    cartSum: function () {
      let sum = 0;
      for (const key in this.cart) {
        sum += this.cart[key].product.price * this.cart[key].qty;
      }
      return sum;
    },
  },
  methods: {
    sliderStatus: function () {
      return this.slider = !this.slider;
    },
    addItems: function (items) {
      let itemCompare;
      let cartProducts = this.cart.filter(function (cart, index) {
        if (cart.product.id == Number(items.id)) {
          itemCompare = index;
          return true;
        } else {
          return false;
        }
      });

      if (cartProducts.length) {
        this.cart[itemCompare].qty++;
      } else {
        this.cart.push({
          product: items,
          qty: 1
        });
      }
    },
    deleteItems: function (index) {
      if (this.cart[index].qty > 1) {
        this.cart[index].qty--;
      } else {
        this.cart.splice(index, 1);
      }
    }
  }
}
</script>
