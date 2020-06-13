<template>
  <div class="restaurant-item">
    <v-row no-gutters>
      <v-col cols="12" sm="3">
        <div class="restaurant-item__logo">
          <v-img :src="restaurant.Logo" :height="150" :width="150" contain :alt="restaurant.Name" />
        </div>
      </v-col>
      <v-col cols="12" sm="7">
        <div class="restaurant-item__description">
          <div>
            <div class="restaurant-item__description__name">
              <span>{{ restaurant.Name }}</span>
            </div>
            <div class="restaurant-item__description__rating">
              <v-icon>thumb_up</v-icon>
              <span>{{ returnRating }}%</span>
            </div>
          </div>
          <div class="restaurant-item__description__tags">
            {{ returnSpecializations }}
          </div>
          <div class="restaurant-item__description__buttons">
            <v-btn text>Меню</v-btn>
            <v-btn text>Инфо</v-btn>
            <v-btn text>Отзывы ({{ restaurant.ReviewsCount }})</v-btn>
          </div>
        </div>
      </v-col>
      <v-col cols="12" sm="2">
        <div class="restaurant-item__prices">
          <div class="restaurant-item__prices__item">
            <span>{{ restaurant.DeliveryCost }}</span>
            <span>Мин сумма заказа</span>
          </div>
          <div class="restaurant-item__prices__item">
            <span>{{ restaurant.DeliveryCost }}</span>
            <span>Стоимость доставки</span>
          </div>
          <div class="restaurant-item__prices__item">
            <span>{{ restaurant.DeliveryCost }}</span>
            <span>Время доставки</span>
          </div>
        </div>
      </v-col>
    </v-row>
  </div>
</template>

<script>
export default {
  name: 'RestourantsItem',
  props: {
    restaurant: {
      type: Object,
      default: () => ({})
    }
  },
  computed: {
    returnSpecializations () {
      return this.restaurant.Specializations.map(x => x.Name).join(' / ')
    },
    returnRating () {
      return Math.round(this.restaurant.PositiveReviews / this.restaurant.ReviewsCount * 100)
    }
  }
}
</script>

<style lang="scss">
  .restaurant-item {
    width: 100%;
    border: 1px solid #ccc;
    border-radius: 10px;
    margin-bottom: 20px;

    &__logo {
      display: flex;
      align-items: center;
      height: 100%;
    }

    &__description {
      padding: 10px;
      display: flex;
      align-items: baseline;
      height: 100%;
      flex-direction: column;
      justify-content: space-between;

      &__rating, &__name {
        display: inline-block;
      }

      &__rating {
        margin-left: 20px;
        color: #4aa500;

        .v-icon {
          font-size: 16px;
          color: #4aa500;
        }
      }

      &__tags {
        color: #ccc;
        margin-top: 10px;
        font-size: 12px;
      }

      &__buttons {
        margin-left: -16px;
      }
    }

    &__prices {
      padding: 10px;

      &__item {
        text-align: center;

        span {
          display: block;
        }

        span:first-child {
          font-size: 20px;
          font-weight: bold;
        }

        span:last-child {
          font-size: 12px;
        }
      }
    }
  }

  @media only screen and (max-width: 600px) {
    .restaurant-item__description {
      align-items: center;
    }
  }

</style>
