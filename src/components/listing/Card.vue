<template>
  <div class="listing-wrapper">

    <div class="list-title">
      <div class="row">
        <div class="col-sm">
          <div class="list-title-arrow">
            >
          </div>
        </div>
        <div class="col-sm">{{ this.title }}</div>
        <div class="col-sm">
          <div class="list-title-total">
            {{ response.listing.length }}
          </div>
        </div>
      </div>
    </div>

    <div class="listing-card" v-for="(list, index) in response.listing" :key="index">

      <div class="card-head">
        <div class="row">
          <div class="col-sm">
            <div class="card-title">REF/PO:</div>
            <div>{{ list.load_ref }}</div>
          </div>
          <div class="col-sm">
            <div class="card-title">To Pickup</div>
            <div>{{ list.created_at }}</div>
          </div>
        </div>
      </div>

      <div class="card-body">
        <div class="row">
          <div class="col-sm">
            <div>Order {{ list.order_number }}</div>
          </div>
        </div>

        <div class="row">
          <div class="col-sm">
            <div class="card-title">Created at</div>
            <div>{{ list.created_at }}</div>
          </div>
        </div>

        <div class="row">
          <div class="col-sm">
            <div class="card-title">Customer Name</div>
            <div>{{ list.customer_name }}</div>
          </div>
          <div class="col-sm">
            <div class="card-title">Phone Number</div>
            <div>{{ list.phone_number }}</div>
          </div>
        </div>

        <div class="row">
          <div class="col-sm">
            <div class="card-title">Price to Customer</div>
            <div>{{ list.order_price_formatted }}</div>
          </div>
          <div class="col-sm">
            <div class="card-title">Tahmeel Fee</div>
            <div>{{ list.tahmeel_fee_in_cents }}</div>
          </div>
        </div>
      </div>

    </div>

  </div>
</template>
<script>
import axios from 'axios'

export default {
  props: {
    title: {
      required: true,
      type: String
    },
    id: {
      required: true,
      type: String
    },
    config: {
      required: true,
      type: Object
    }
  },
  data() {
    return {
      response: {
        listing: [],
        loading: true,
        error: false
      }
    }
  },
  methods: {
    getListing() {

      axios(this.config).then(response => {
        this.response.listing = response.data[this.id]
        this.response.loading = false

        console.log("this.response.listing");
        console.log(this.response.listing);
      }).catch(e => {
        console.log(e);
        this.response.loading = false
        this.response.error = true
      })

    }
  },
  mounted() {
    this.getListing();
  }
}
</script>
<style lang="scss" scoped>
.listing-wrapper {
  background-color: #2A2A2A;
  border: 1px solid #0B0B0B;

  .list-title {
    color: #FFFFFF;
  }

  .listing-card {
    .card-head {
      background-color: #FFFFFF;
    }

    .card-body {
      color: #FFFFFF;
    }

    .card-title {

    }
  }
}
// #5ADCC0
// #545454
// #2A2A2A
</style>
