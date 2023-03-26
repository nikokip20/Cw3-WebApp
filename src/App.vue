
<template>
  <div id="app">
    <button v-on:click="toggleBasket">{{cartItemCount}} Checkout</button> 



    <main>
      <component :is="currentView" :sortedProducts="sortedProducts" :cart="cart" @add-item-to-cart="addToCart" @remove-item-event="removeItem" :details="details"> </component>
    </main>
  </div>
</template>

<script>

import ProductList from './components/ProductList.vue';
import Checkout from './components/Checkout.vue';
import products from "./assets/json/subject.json";
import style from "./assets/style.css"

export default {
  name: 'app',

  data() {
    return {

      cart: [],
      products: products,
      currentView: ProductList,
      details: {
            name: "",
            surname: "",
            address: "",
            phoneNo: "",
 }

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
    addToCart(products) {
      this.cart.push(products.productID);  //adds product to cart array


    },
    canAddToCart(products) {
      return products.Space > this.cartCount(products.productID);   //functuion enables and disables the button if product in stock

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

    removeItemCart(products){
      let i = this.cart.indexOf(products.productID);
      // remove the item that the index is pointing to
      this.cart.splice(i,1);
    },
    removeItem(products){
      this.removeItemCart(products);
    },  
    returnDetails(details){
      return details;
    }
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