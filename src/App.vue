<template>
  <div id="app-wrapper">
    <div class="container">
      <div class="row">
        <div class="col-xs-12 col-md-4" v-for="(list, index) in listing" :key="index">
          <listing-card :title="list.title" :id="list.id" :config="list.config" />
        </div>
      </div>
    </div>
  </div>
</template>

<script>

import ListingCard from "./components/listing/Card.vue";

export default {
  name: "App",
  components: {
    ListingCard
  },
  data() {
    return {
      listing: [
        {
          title: 'Pending',
          id: 'pending_orders',
          config: {
            url: 'https://api.stagingtahmeelapp.com/technical_interview/orders/pending',
            method: 'GET'
          }
        },
        {
          title: 'Assigned',
          id: 'assigned_orders',
          config: {
            url: 'https://api.stagingtahmeelapp.com/technical_interview/orders/assigned',
            method: 'GET'
          }
        }
      ]
    }
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;

}
#app-wrapper {
  background-color: #2A2A2A;
  padding: 20px 0;
}
</style>
