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
#app-wrapper {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  padding: 20px 0;
  height: 100vh;
}

::-webkit-scrollbar {
    width: 7px;
}

::-webkit-scrollbar-track {
  visibility: hidden;
}

::-webkit-scrollbar-thumb {
    border-radius: 4px;
    background: rgba(90,220,192,1);
}

</style>
