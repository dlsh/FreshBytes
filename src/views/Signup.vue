<template>
  <div class="signup">
    <div class="columns is-centered">
      <div class="column is-narrow">
        <img
          src="../assets/img/FreshBytesLogo.png"
          height="300px"
          width="300px"
        />
        <div v-if="customer">
          <h1 class="title is-3">Sign Up</h1>
          <h1 class="subtitle is-5">Start Shopping with us today!</h1>
          <customer-signup />
        </div>
        <div v-if="business">
          <h1 class="title is-3">Sign Up</h1>
          <h1 class="subtitle is-5">Start your business with us today!</h1>
          <business-signup />
        </div>
      </div>
    </div>
    <div v-if="!customer && !business">
      <h1 class="title is-3">Sign Up</h1>
      <h1 class="subtitle is-6">Join us and make a difference today!</h1>
      <h1 class="title is-4">Select Your Account Type</h1>
      <div class="columns is-centered buttons">
        <div class="column card-image">
          <figure class="image is-1by1">
            <button v-on:click="toggleCustomer">
              <img :src="CustomerImage" id="buttonimg" />
            </button>
          </figure>
          <b-button
            focused
            type="is-primary"
            expanded
            v-on:click="toggleCustomer"
          >
            Customer
          </b-button>
        </div>
        <div class="column card-image">
          <figure class="image is-1by1">
            <button v-on:click="toggleBusiness">
              <img :src="BusinessImage" id="buttonimg" />
            </button>
          </figure>
          <b-button
            focused
            type="is-danger"
            expanded
            v-on:click="toggleBusiness"
          >
            Business
          </b-button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import CustomerSignup from "../components/signups/CustomerSignup.vue";
import BusinessSignup from "../components/signups/BusinessSignup.vue";
import BusinessImage from "../assets/designs/businessman.png";
import CustomerImage from "../assets/designs/shopping.jpeg";
export default {
  components: {
    CustomerSignup,
    BusinessSignup,
  },
  data: function () {
    return {
      customer: false,
      business: false,
      BusinessImage: BusinessImage,
      CustomerImage: CustomerImage,
    };
  },
  methods: {
    toggleCustomer: function () {
      this.business = false;
      this.customer = true;
    },
    toggleBusiness: function () {
      this.customer = false;
      this.business = true;
    },
  },
};
</script>

<style scoped>
.signup {
  padding-bottom: 100px;
}
button {
  margin-top: 5px;
}
#buttonimg {
  border: 3px solid #8c906d;
  border-radius: 20%;
}
.buttons {
  max-width: 600px;
  margin: auto;
}
.card-image {
  margin: auto;
}
</style>
