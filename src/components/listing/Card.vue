<template>
  <div class="listing-card">

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
.listing-card {

}
</style>
