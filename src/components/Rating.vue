<template>
  <div>
    <h1>Rating: {{ rating }}</h1>
    <div class="stars-container">
      <span
        v-for="star in stars"
        :key="star"
        @mouseover="hoverRating(star)"
        @click="selectRating(star)"
        @mouseleave="resetHoveredRating()"
      >
        <i
          class="bi"
          :class="{ 'bi-star-fill': hoveredRating >= star, 'bi-star': hoveredRating < star }"
        ></i>
      </span>
    </div>
    <div class="rating-info" v-if="selectedRating !== null">
      Durchschnittliche Bewertung: {{ calculateAverageRating().toFixed(1) }}/5
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      hoveredRating: null,
      selectedRating: null,
      totalRatings: 0,
      totalRatingSum: 0,
    };
  },
  methods: {
    hoverRating(star) {
      this.hoveredRating = star;
    },
    selectRating(star) {
      this.selectedRating = star;
      this.totalRatingSum += star;
      this.totalRatings++;
      this.resetHoveredRating();
    },
    resetHoveredRating() {
      this.hoveredRating = null;
    },
    calculateAverageRating() {
      if (this.totalRatings === 0) {
        return 0;
      }
      return this.totalRatingSum / this.totalRatings;
    },
  },
  computed: {
    stars() {
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
