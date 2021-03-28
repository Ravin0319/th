<template>
  <div id="app-wrapper">
    <div class="container">
      <listing-card/>
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
          id: 'pending',
          config: {
            endpoint: 'https://api.stagingtahmeelapp.com/technical_interview/orders/pending',
            method: 'GET'
          }
        },
        {
          title: 'Assigned',
          id: 'assigned',
          config: {
            endpoint: 'https://api.stagingtahmeelapp.com/technical_interview/orders/assigned',
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
  color: #2c3e50;
  margin-top: 60px;
}
</style>
