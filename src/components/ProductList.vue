
<template>
    <div>
        <h1>Product view is working</h1>

            <div v-for="product in sortedProducts" class="main">
               
               
                <div class="itemBox">
                    <p class="home">Subject: {{product.Subject}}</p>
                    <p class="home">Location: {{product.Location}} </p>
                    <p class="home">Price: {{product.Price}}</p>
                      <span class="home" v-if="itemleft(product)>=1">Space: {{itemleft(product)}}</span>
                    <span class="home" v-else>Out of stock</span>
                    <img v-bind:src="product.image">


                    <button v-if="canAddToCart(product)" v-on:click="addItemToCart(product)">Add to cart</button>
                    <button v-else disabeled>Out of stock</button>

                </div>
                <!--End of div for products-->
            </div>

    </div>



</template>
<script>
export default{
    name: "ProductList",
    props:["sortedProducts", "cart"],
    data(){
        return{

        }
    },
    methods: {
        itemleft(product) {
            return product.Space - this.cartCount(product.productID);
        },  //we use this funtion to determine the remaining spaces in the product

        canAddToCart(product) {
            return product.Space > this.cartCount(product.productID);

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
    addItemToCart: function(product){
        this.$emit("add-item-to-cart", product);
    }
     
}
}
</script>