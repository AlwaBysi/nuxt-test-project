<template>
  <div>
    <v-row no-gutters>
      <v-col cols="12" md="4" v-for="i in showCount" :key="i" :review="reviews[i]">
        <reviews-item :review="reviews[i]" :restaurants="restaurants"/>
      </v-col>
    </v-row>
    <v-btn depressed block color="primary" @click="showMore">Показать еще</v-btn>
  </div>
</template>

<script>
import ShowMoreData from '@/mixins/ShowMoreData'
import ReviewsItem from '@/components/ReviewsItem'

export default {
  name: 'reviews',
  mixins: [ShowMoreData],
  components: {
    ReviewsItem
  },
  props: {
    reviews: {
      type: Array,
      default: () => ([])
    },
    restaurants: {
      type: Array,
      default: () => ([])
    }
  },
  methods: {
    showMore () {
      /*eslint-disable*/
      if (this.showCount === this.reviews.length) return;
      this.showCount += this.stepsCount;
      if (this.showCount > this.reviews.length) this.showCount = this.reviews.length;
    }
  }
}
</script>
