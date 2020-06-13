<template>
  <v-card class="ma-2 mt-3">
    <v-img :src="hit.ProductImage" height="200px" />
    <v-card-title>{{ hit.ProductName }}</v-card-title>
    <v-card-subtitle>
      {{ hit.ProductPrice }} &#8381;
    </v-card-subtitle>
    <v-card-text>
      {{ hit.ProductDescription }}
    </v-card-text>
    <v-card-actions>
      <v-btn text>Купить</v-btn>
    </v-card-actions>
  </v-card>
</template>

<script>
export default {
  name: 'HitsItem',
  props: {
    hit: {
      type: Object,
      default: () => ({})
    }
  },
  data: () => ({
    show: false,
    count: 1
  }),
  methods: {
    increment () {
      ++this.count
    },
    decrement () {
      /*eslint-disable*/
      if (this.count === 0) return
      --this.count
    }
  }
}
</script>

<style scoped lang="scss">
  .v-input {
    width: 30px;
  }
</style>
