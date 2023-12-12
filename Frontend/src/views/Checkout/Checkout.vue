<template>
  <div class="div_class">
    <h3>You will be redirected to payment page</h3>
    <button
      class="checkout_button"
      id="proceed-to-checkout"
      @click="goToCheckout()"
    >
      Make payment
    </button>
  </div>
</template>
<script>
export default {
  data() {
    return {
      stripeAPIToken:'pk_test_51MYGLMFGwibAvTNjtNbOkB4N6TnnrxzLWw1OdmjncrqAvwyyEfRSJGd4fWiPrwgZJJiKOL0HISoOi4jSYyROYTuv00E2wO3oC5',
      stripe: '',
      token: null,
      sessionId: null,
      checkoutBodyArray: [],
    };
  },

  name: 'Checkout',
  props: ['baseURL'],
  methods: {
    /*
      Configures Stripe by setting up the elements and
      creating the card element.
    */
    configureStripe() {},

    getAllItems() {
      axios.get(`${this.baseURL}cart/?token=${this.token}`).then(
        (response) => {
          if (response.status == 200) {
            let products = response.data;
            let len = Object.keys(products.cartItems).length;
            for (let i = 0; i < len; i++)
              this.checkoutBodyArray.push({
                imageUrl: products.cartItems[i].product.imageURL,
                productName: products.cartItems[i].product.name,
                quantity: products.cartItems[i].quantity,
                price: products.cartItems[i].product.price,
                productId: products.cartItems[i].product.id,
                userId: products.cartItems[i].userId,
              });
          }
        },
        (err) => {
          console.log(err);
        }
      );
    },

    goToCheckout() {
      axios
        .post(
          this.baseURL + 'order/create-checkout-session',
          this.checkoutBodyArray
        )
        .then((response) => {
          localStorage.setItem('sessionId', response.data.sessionId);
          return response.data;
        })
        .then((session) => {
          return this.stripe.redirectToCheckout({
            sessionId: session.sessionId,
          });
        });
    },
  },
  mounted() {
    // get the token
    this.token = localStorage.getItem('token');
    // get all the cart items
    this.stripe = Stripe(this.stripeAPIToken);
    this.getAllItems();
  },
};
</script>

<style>
.alert {
  width: 50%;
}

.div_class {
  text-align: center;
  padding-top: 10%;
}

.checkout_button {
  background-color: #febd69;
  border: none;
  color: white;
  padding: 15px 30px;
  margin: 4%;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 15px;
  font-weight: bold;
  border-radius: 15px;
}

.checkout_button:focus {
  outline: none;
  box-shadow: none;
}

.checkout_button:disabled {
  background-color: #9b86f7;
  border: none;
  color: white;
  margin-left: 15%;
  padding: 15px 30px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 15px;
  font-weight: bold;
  border-radius: 15px;
  cursor: not-allowed;
}
@media (max-width:400px) {
  .div_class {
    text-align: center;
    padding-top: 30%;
  }
}
</style>
