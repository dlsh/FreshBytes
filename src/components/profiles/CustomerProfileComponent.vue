<template>
  <div>
    <section class="hero is-small">
      <div class="hero-body">
        <img :src="ProfilePic" />
        <p class="title">
          {{ userDetails.name }}
        </p>
      </div>
    </section>

    <div class="columns">
      <div class="column is-2">
        <side-bar v-on:change-profile="changeDetails"></side-bar>
      </div>
      <div class="column">
        <div id="content">
          <user-details
            v-bind:userDetails="userDetails"
            v-bind:isCustomer="isCustomer"
            v-bind:userId="userDetails.id"
            v-if="toShow.details"
          ></user-details>
          <order-details
            v-bind:allOrders="allOrders"
            v-if="toShow.orders"
          ></order-details>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import SideBar from "../SideBar.vue";
import OrderDetails from "../OrderDetails.vue";
import UserDetails from "../UserDetails.vue";
import ProfilePic from "../../assets/img/profile.png";
import { getUserOrdersWithListing } from "../../database/queries";

export default {
  components: {
    SideBar,
    OrderDetails,
    UserDetails,
  },
  data() {
    return {
      allOrders: [],
      toShow: {
        details: true,
        orders: false,
        dashboard: false,
      },
      ProfilePic: ProfilePic,
    };
  },
  methods: {
    /**
     * Changes the displayed element in the profile page based on a click on the sidebar
     */
    changeDetails: function (event) {
      for (const property in this.toShow) {
        this.toShow[property] = property == event ? true : false;
      }
    },
  },
  computed: {
    userDetails: function () {
      return this.$store.getters.getUserData;
    },
    isCustomer: function () {
      return this.$store.getters.isCustomer;
    },
  },
  created: async function () {
    this.allOrders = await getUserOrdersWithListing(true, this.userDetails.id);
  },
};
</script>

<style scoped>
#content {
  margin-left: 50px;
  padding: 1px 16px;
}
</style>
