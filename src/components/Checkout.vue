<template>
    <div>
        <h2>Checkout view is working</h2>

        <p>Your total items in cart are: {{ cartItemCount }} </p>

        <div v-for="product in sortedProducts" class="main">
       
            <div v-if="itemInCart(product)">
         <div class="itemBox">
                <h3 v-text="product.Subject"></h3>
                <div>
                    <p><span>Product ID:</span>{{ " " + product.productID }}</p>
                    <img v-bind:src="product.image">
                    <p>In cart you have added:
                        {{ cartCount(product.productID) }}
                        <button v-on:click="removeItem(product)">Remove one</button>
                    </p>
                    
                </div>

        </div>


            </div>
        </div>
        <!-- <strong>Name:</strong>
            <input type="name" v-model.trim="details.name">

            <strong>Surname:</strong>
            <input type="name" v-model.trim="details.surname">

            <strong>PhoneNo:</strong>
            <input type="number" v-model.trim="details.phoneNo">

            <strong>Address:</strong>
            <input type="name" v-model.trim="details.address"> -->




    </div>
</template>
<script>
export default {
    name: "Checkout",

    props: ["sortedProducts", "cart"],
    data() {
        return {

        }
    },

    methods: {
        itemInCart: function(product){
            return this.cart.includes(product.productID);
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
    
    removeItem: function(product){
        this.$emit("remove-item-event", product);
    }

},
    computed: {
        cartItemCount: function () {
            return this.cart.length || "";
        },
    }

  
}   
</script>