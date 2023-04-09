<template>
  <div class="about">
    <div class="container">
      <div class="row">
        <div class="col-md-4">
          <div class="card mt-4">
            <div align="center">
              <img class="user-image mt-4" src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTot6pKUgJZYElkKVz8GRAPwGsdsa7ETMvMhQ&usqp=CAU" alt="logo"/>
            <div class="mt-3 ml-5">Name : Kurta Set</div>
            <div class="mt-1 ml-5">Price : Rs.2000</div>
              <stripe-checkout
                ref="checkoutRef"
                mode="payment"
                :pk="publishableKey"
                :line-items="lineItems"
                :success-url="successURL"
                :cancel-url="cancelURL"
                @loading="v => loading = v"
              />
            <button type="button" class="btn btn-success  my-3" v-on:click="submit">Buy Now</button>
            </div>
            
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import { StripeCheckout } from '@vue-stripe/vue-stripe';
export default {
  components: {
    StripeCheckout,
  },
  data () {
    this.publishableKey = "pk_test_51LibL9SGiNiACACCZ4SSZGmUiPuPkCegJ44rcasnQghxH9D5JwH5K5YAC4cor3BsZgbpLA1fJzQP9Katc5QoBUXO00EZmgWJms";
    return {
      loading: false,
      lineItems: [
        {
          price: 'price_1LibQfSGiNiACACCzG5Cgd1e', 
          quantity: 1,
        },
      ],
      successURL: 'http://localhost:8080/success',
      cancelURL: 'http://localhost:8080/error',
    };
  },
  methods: {
    submit() {
      // You will be redirected to Stripe's secure checkout page
      this.$refs.checkoutRef.redirectToCheckout();
    },
  },
};
</script>
<style>
.card-class{
  width: 110px;
}
.user-image{
  width: 300px;
   height: 300px;
}
</style>
