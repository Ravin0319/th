<template>
  <div id="">
    card
  </div>
</template>
<script>
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
    }
  },
  mounted() {
    console.log(this.title);
    console.log(this.id);
    console.log(this.config);
  }
}
</script>
<style lang="scss" scoped>
</style>
