<template>
  <div>
    <v-row no-gutters>
      <v-col cols="12" md="4" v-for="i in showCount" :key="hits[i].Name">
        <hits-item :hit="hits[i]" />
      </v-col>
    </v-row>
    <v-btn depressed block color="primary" @click="showMore">Показать еще</v-btn>
  </div>
</template>

<script>
import HitsItem from '@/components/HitsItem'
import ShowMoreData from '@/mixins/ShowMoreData'

export default {
  name: 'Hits',
  mixins: [ShowMoreData],
  components: {
    HitsItem
  },
  props: {
    hits: {
      type: Array,
      default: () => ([])
    }
  },
  methods: {
    showMore () {
      /*eslint-disable*/
      if (this.showCount === this.hits.length) return;
      this.showCount += this.stepsCount;
      if (this.showCount > this.hits.length) this.showCount = this.hits.length;
    }
  }
}
</script>
