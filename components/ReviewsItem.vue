<template>
  <v-card
      class="ma-2 mt-3 review-item"
  >
    <v-img
        class="white--text align-end"
        height="200px"
        :src="returnSrc"
    />

    <div class="review-item__thumb">
      <v-icon v-if="review.IsPositive" class="review-item__thumb_up">thumb_up</v-icon>
      <v-icon v-else class="review-item__thumb_down">thumb_down</v-icon>
    </div>

    <v-card-subtitle class="pb-0">{{ returnDateAdded }}</v-card-subtitle>

    <v-card-text class="text--primary">
      <div>{{ review.UserFIO }}</div>
      <div>{{ review.Message }}</div>
    </v-card-text>
  </v-card>
</template>

<script>
export default {
  name: 'ReviewsItem',
  props: {
    review: {
      type: Object,
      default: () => ({})
    },
    restaurants: {
      type: Array,
      default: () => ([])
    }
  },
  data: () => ({
    defaultImg: 'https://cdn.vuetifyjs.com/images/cards/docks.jpg'
  }),
  computed: {
    returnDateAdded () {
      return this.$moment(this.review.DateAdded).format('DD MM YYYY')
    },
    returnSrc () {
      const restaurants = this.restaurants.find(x => x.Name === this.review.RestaurantName)
      return restaurants ? restaurants.Logo : this.defaultImg
    }
  }
}
</script>

<style scoped lang="scss">
  .review-item {
    &__thumb {
      padding: 10px 0 0 15px;
      &_up {
        color: green
      }
      &_down {
        color: red
      }
    }
  }
</style>
