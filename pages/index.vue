<template>
  <div>
    <v-container>
      <v-card>
        <v-toolbar class="mt-3 pt-3">
          <v-text-field label="Поиск заведения" v-model="filter"></v-text-field>
        </v-toolbar>
      </v-card>
    </v-container>
    <v-container>
      <v-card>
        <v-row>
          <v-col cols="12" sm="6" md="3" v-for="item in checkboxes" :key="item.id">
            <v-checkbox v-model="item.model" :label="item.label" @click="changeCheckbox(item)"></v-checkbox>
          </v-col>
        </v-row>
      </v-card>
    </v-container>
    <v-container>
      <h2 class="mt-5">Рестораны</h2>
      <restaurants :restaurants="restaurantsItems" :filtered-restaurants="filteredRestaurants" :filter="filtering" />
      <h2 class="mt-5">Хиты продаж</h2>
      <hits :hits="hits" />
      <h2 class="mt-5">Отзывы</h2>
      <reviews :reviews="reviews" :restaurants="restaurantsItems" />
    </v-container>
  </div>
</template>

<script>
import axios from 'axios'
import Restaurants from '@/components/Restaurants'
import Hits from '@/components/Hits'
import Reviews from '@/components/Reviews'

export default {
  components: {
    Restaurants,
    Hits,
    Reviews
  },
  async asyncData () {
    const restaurants = await axios.get('https://front-task.chibbistest.ru/api/v1/restaurants').catch(() => ({ data: [] }))
    const hits = await axios.get('https://front-task.chibbistest.ru/api/v1/hits').catch(() => ({ data: [] }))
    const reviews = await axios.get('https://front-task.chibbistest.ru/api/v1/reviews').catch(() => ({ data: [] }))
    return { restaurantsItems: restaurants.data, hits: hits.data, reviews: reviews.data }
  },
  data: () => ({
    filteredRestaurants: [],
    filter: null,
    filtering: false,
    checkboxes: [
      {
        label: 'Пицца',
        model: false,
        id: 1
      },
      {
        label: 'Суши',
        model: false,
        id: 2
      },
      {
        label: 'Бургеры',
        model: false,
        id: 3
      },
      {
        label: 'Пироги',
        model: false,
        id: 4
      }
    ]
  }),
  methods: {
    changeCheckbox () {
      /*eslint-disable*/
      const filterArr = []

      for (let i = 0; i < this.checkboxes.length; i++) {
        if (this.checkboxes[i].model) filterArr.push(this.checkboxes[i].label)
      }

      if (!filterArr.length) {
        this.filtering = false
        this.filteredRestaurants = []
        return
      }

      this.filteredRestaurants = this.restaurantsItems.filter(x => {
        for (let i = 0; i < filterArr.length; i++) {
          if (x.Specializations.find(y => y.Name === filterArr[i])) return x
        }
      })
    }
  },
  watch: {
    filter (newVal) {
      if (newVal && newVal.length) {
        for (let i = 0; i < this.checkboxes.length; i++) {
          if (this.checkboxes[i].model) this.$set(this.checkboxes[i], 'model', false)
        }

        this.filtering = true

        const results = this.restaurantsItems.filter(x => x.Name.includes(newVal))

        if (results) {
          this.filteredRestaurants = results
        } else {
          this.filteredRestaurants = []
        }
      } else {
        this.filtering = false
        this.filteredRestaurants = []
      }
    }
  }
}
</script>
