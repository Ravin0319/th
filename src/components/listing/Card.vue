<template>
  <div>

    <div v-if="response.loading">
      <spinner/>
    </div>

    <div class="listing-wrapper" v-else-if="!response.loading && !response.error">

      <div class="list-title-wrapper">
        <div class="row">
          <div class="col">
            <div class="list-title-arrow">
              <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" fill="currentColor" class="bi bi-chevron-down" viewBox="0 0 16 16">
                <path fill-rule="evenodd" d="M1.646 4.646a.5.5 0 0 1 .708 0L8 10.293l5.646-5.647a.5.5 0 0 1 .708.708l-6 6a.5.5 0 0 1-.708 0l-6-6a.5.5 0 0 1 0-.708z"/>
              </svg>
            </div>
          </div>
          <div class="col list-title text-center align-self-center">{{ this.title }}</div>
          <div class="col">
            <div class="list-title-total float-right">
              {{ response.listing.length }}
            </div>
          </div>
        </div>
      </div>

      <div class="listing-card" v-for="(list, index) in response.listing" :key="index">

        <div class="card-head">
          <div class="row">
            <div class="col">
              <div class="card-label">Ref/Po:</div>
              <div class="card-value">{{ list.load_ref }}</div>
            </div>
            <div class="col text-right">
              <div class="card-label" v-if="id === 'assigned_orders'">To Pickup</div>
              <div class="card-value">
                <!-- {{ list.created_at }} -->
                JAN 5
              </div>
            </div>
          </div>
        </div>

        <div class="card-body">

          <div class="row mb-2">
            <div class="col text-center">
              <div class="card-value">Order {{ list.order_number }}</div>
            </div>
          </div>

          <div class="row mb-2">
            <div class="col text-center">
              <div class="card-label">Created at</div>
              <div class="card-value">{{ list.created_at }}</div>
            </div>
          </div>

          <div class="row mb-2">
            <div class="col text-center">
              <div class="card-label">Customer Name</div>
              <div class="card-value">{{ list.customer_name }}</div>
            </div>
            <div class="col text-center">
              <div class="card-label">Phone Number</div>
              <div class="card-value">{{ list.phone_number }}</div>
            </div>
          </div>

          <div class="row">
            <div class="col text-center">
              <div class="card-label">Price to Customer</div>
              <div class="card-value">{{ list.order_price_formatted }}</div>
            </div>
            <div class="col text-center">
              <div class="card-label">Tahmeel Fee</div>
              <div class="card-value">{{ list.tahmeel_fee_in_cents }}</div>
            </div>
          </div>

        </div>

      </div>

    </div>

    <div v-else>
      <div class="row">
        <div class="col text-center">
          <div class="error-text">
            Sorry something is wrong, Please try again later
          </div>
        </div>
      </div>
    </div>

  </div>
</template>
<script>
import axios from 'axios'
import Spinner from './Spinner.vue'

export default {
  components: {
    Spinner
  },
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
  border: 1px solid #545454;
  padding: 10px;
  border-radius: 6px;

  //Title - Accordion
  .list-title-wrapper {
    color: #FFFFFF;
    border-bottom: 3px solid #5ADCC0;
    margin-bottom: 10px;
    .list-title-arrow {

    }
    .list-title {
      text-transform: uppercase;
    }
    .list-title-total {
      background-color: #5ADCC0;
      margin: 5px;
      border-radius: 5px;
      padding: 0 7.5px;
    }
  }
  //Title - Accordion

  //Listing Card
  .listing-card {
    background-color: #545454;
    margin-top: 5px;
    border-radius: 5px;

    //Card Head
    .card-head {
      background-color: #FFFFFF;
      padding: 5px 10px;
      border-top-right-radius: 5px;
      border-top-left-radius: 5px;
      font-size: 12px;

      .card-label {
        color: #545454;
        font-size: 12px;
        font-weight: 400;
        margin-bottom: 5px;
      }

      .card-value {
        color: #545454;
        font-size: 12px;
        font-weight: 400;
      }

    }
    //Card Head

    .card-body {
      color: #FFFFFF;
    }

    .card-label {
      text-transform: uppercase;
      font-size: 10px;
      font-weight: 200;
    }

    .card-value {
      font-size: 14px;
      font-weight: 300;
    }
  }
  //Listing Card

}

.loading-text, .error-text {
  color: #ffffff;
  font-size: 12px;
  margin: 5px;
}
</style>
