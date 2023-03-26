
<template>
  <div id="app">
    <button v-on:click="toggleBasket">{{cartItemCount}} Checkout</button> 



    <main>
      <component :is="currentView" :sortedProducts="sortedProducts" :cart="cart" @add-item-to-cart="addToCart"> </component>
    </main>
  </div>
</template>

<script>

import ProductList from './components/ProductList.vue';
import Checkout from './components/Checkout.vue';
import products from "./assets/json/subject.json";

export default {
  name: 'app',

  data() {
    return {

      cart: [],
      products: products,
      currentView: ProductList,

    }
  },
  components: { ProductList, Checkout },
  methods: {

    toggleBasket() {
      if (this.currentView === ProductList) {
        this.currentView = Checkout;
      } else {
        this.currentView = ProductList;
      }
    },
    addToCart(product) {
      this.cart.push(product.productID);  //adds product to cart array


    },
    canAddToCart(product) {
      return product.Space > this.cartCount(product.productID);   //functuion enables and disables the button if product in stock

    },

    cartCount(productID) {
      let count = 0;
      for (let i = 0; i < this.cart.length; i++) {
        if (this.cart[i] === productID) {
          count++;

        }

      }
      return count;//cheching for the item that we are going to add to the cart 
    },

    
  },
  computed: {
    cartItemCount: function () {
      return this.cart.length || "";
    },

    sortedProducts(){

      function compare(a, b){
        if(a.Price > b.Price) return +1;
        if(a.Price <b.Price) return -1;
        return 0;
      
      }
      return this.products.sort(compare);
    }
  }

}
</script>