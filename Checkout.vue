<template>
    <div>
        <h2>Checkout page</h2>

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
        <strong>Name:</strong>
            <input type="name" v-model.trim="details.name">

            <strong>Surname:</strong>
            <input type="name" v-model.trim="details.surname">

            <strong>PhoneNo:</strong>
            <input type="number" v-model.trim="details.phoneNo">

            <strong>Address:</strong>
            <input type="name" v-model.trim="details.address"> 



            <h3>Order Details:</h3>
            <p>Name: {{details.name}}</p>
            <p>Surname: {{details.surname}}</p>
            <p>PhoneNo: {{details.phoneNO}}</p>
            <p>Address : {{details.address}}</p>
            <!--Displaying the data that the user entered-->
            <button v-on:click="submitForm(details)">Place order</button>
        </div>
        <!--End of div for checkout-->

    

</template>
<script>
export default {
    name: "Checkout",

    props: ["sortedProducts", "cart", "details"],
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
    },
    submitForm(details) {
            if (details.phoneNo <= 0) {
                alert("Please enter a valid phone number");
            }
            else if (details.name === "") {
                alert("Enter a valid name");
            }
            else if (details.address === "") {
                alert("Enter a valid address!");
            }
            else {
                alert("Order confirmed!");
            }   //with this function we make sure the user fills out the form before cheching out

},
    computed: {
        cartItemCount: function () {
            return this.cart.length || "";
        },
    }

  
}   
}
</script>