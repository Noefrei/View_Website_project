
<template>
  <div>
    <h1>Rating: {{ mainRating }}</h1>
    <p v-if="totalMainRatings > 0">
      Diese Objekt wurde {{ totalMainRatings }} mal bewertet.
    </p>
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
      starClickCounts: { 1: 0, 2: 0, 3: 0, 4: 0, 5: 0 },
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
      // Zähler erhöhen
      this.starClickCounts[star]++;
      // Speichern im localStorage
      localStorage.setItem('mainRating', JSON.stringify({
        totalRatings: this.totalMainRatings,
        totalRatingSum: this.totalMainRatingSum,
        starClickCounts: this.starClickCounts,
      }));
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
    loadStoredRating() {
      // Laden aus dem localStorage
      const storedRating = localStorage.getItem('mainRating');
      if (storedRating) {
        const { totalRatings, totalRatingSum, starClickCounts } = JSON.parse(storedRating);
        this.totalMainRatings = totalRatings;
        this.totalMainRatingSum = totalRatingSum;
        this.starClickCounts = starClickCounts;
      }
    },
  },
  computed: {
    mainStars() {
      return [1, 2, 3, 4, 5];
    },
    mainRating() {
      return this.calculateMainAverageRating().toFixed(1);
    },
  },
  mounted() {
    this.loadStoredRating();
  },
  beforeDestroy() {
    localStorage.setItem('mainRating', JSON.stringify({
      totalRatings: this.totalMainRatings,
      totalRatingSum: this.totalMainRatingSum,
      starClickCounts: this.starClickCounts,
    }));
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
  color: orange;
}
.rating-info {
  margin-top: 8px;
}
</style>