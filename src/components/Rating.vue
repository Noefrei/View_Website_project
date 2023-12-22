<template>
  <div>
    <h1>Rating: {{ mainRating }}</h1>
    <div class="stars-container">
      <span
        v-for="star in mainStars"
        :key="star"
        @mouseover="hoverMainRating(star)"
        @click="selectMainRating(star)"
        @mouseleave="resetHoveredMainRating()"
      >
        <i
          class="bi"
          :class="{ 'bi-star-fill': hoveredMainRating >= star, 'bi-star': hoveredMainRating < star }"
        ></i>
      </span>
    </div>
    <div class="rating-info" v-if="selectedMainRating !== null">
      Durchschnittliche Bewertung: {{ calculateMainAverageRating().toFixed(1) }}/5
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      hoveredMainRating: null,
      selectedMainRating: null,
      totalMainRatings: 0,
      totalMainRatingSum: 0,
    };
  },
  methods: {
    hoverMainRating(star) {
      this.hoveredMainRating = star;
    },
    selectMainRating(star) {
      this.selectedMainRating = star;
      this.totalMainRatingSum += star;
      this.totalMainRatings++;
      this.resetHoveredMainRating();
    },
    resetHoveredMainRating() {
      this.hoveredMainRating = null;
    },
    calculateMainAverageRating() {
      if (this.totalMainRatings === 0) {
        return 0;
      }
      return this.totalMainRatingSum / this.totalMainRatings;
    },
  },
  computed: {
    mainStars() {
      return [1, 2, 3, 4, 5];
    },
  },
  components: {
    AmazonRating: {
      props: ['initialRating'],
      data() {
        return {
          rating: this.initialRating,
        };
      },
      methods: {
        assignRating(newRating) {
          this.rating = newRating;
        },
      },
      template: `
        <div class="amazon-rating">
          <span
            v-for="star in stars"
            :key="star"
            @click="assignRating(star)"
          >
            <i
              class="bi"
              :class="{ 'bi-star-fill': rating >= star, 'bi-star': rating < star }"
            ></i>
          </span>
          <div class="rating-info" v-if="rating !== null">
            Durchschnittliche Bewertung: {{ rating.toFixed(1) }}/5
          </div>
        </div>
      `,
    },
  },
};
</script>

<style scoped>
.rating {
  font-size: 24px;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.stars-container {
  display: flex;
}

.stars-container span {
  cursor: pointer;
}

.rating-info {
  margin-top: 8px;
}

.amazon-rating {
  font-size: 18px;
  display: flex;
  flex-direction: column;
  align-items: center;
}
</style>
