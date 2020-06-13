<template>
  <div>
    <div v-if="filter && !filteredRestaurants.length" class="empty-msg">
      <span>Не найдено ни одного ресторана</span>
    </div>
    <div v-else-if="filteredRestaurants.length">
      <restaurants-item v-for="item in filteredRestaurants" :key="item.Name" :restaurant="item" />
    </div>
    <div v-else>
      <restaurants-item v-for="i in showCount" :key="restaurants[i].Name" :restaurant="restaurants[i]" />
    </div>
    <v-btn depressed block color="primary" @click="showMore">Показать еще</v-btn>
  </div>
</template>

<script>
import RestaurantsItem from '@/components/RestourantsItem'
import ShowMoreData from '@/mixins/ShowMoreData'

export default {
  name: 'Restaurants',
  mixins: [ShowMoreData],
  components: {
    RestaurantsItem
  },
  props: {
    restaurants: {
      type: Array,
      default: () => ([])
    },
    filteredRestaurants: {
      type: Array,
      default: () => ([])
    },
    filter: {
      type: Boolean,
      default: false
    }
  },
  methods: {
    showMore () {
      /*eslint-disable*/
      if (this.showCount === this.restaurants.length) return;
      this.showCount += this.stepsCount;
      if (this.showCount > this.restaurants.length) this.showCount = this.restaurants.length;
    }
  }
}
</script>

<style lang="scss">
  .empty-msg {
    display: flex;
    align-items: center;
    justify-content: center;
    height: 300px;
  }
</style>
