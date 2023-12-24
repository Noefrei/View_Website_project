<template>
  <div>
    <button @click="showRatingDistribution">Zeige Rating Verteilung</button>

    <div v-if="showDistribution">
      <canvas ref="ratingChart" width="400" height="200"></canvas>
      <table>
        <thead>
          <tr>
            <th>Sterne</th>
            <th>Anzahl</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(count, star) in ratingCount" :key="star">
            <td>{{ star }} Sterne</td>
            <td>{{ count }}</td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script>
import Chart from 'chart.js/auto';

export default {
  data() {
    return {
      showDistribution: false,
      ratingCount: {},
    };
  },
  methods: {
    showRatingDistribution() {
      // rating mit der Distribution tabelle verküpfen sodass anzahl rating mit den daten tabelle übereinstimmen!
      
      this.ratingCount = this.generateRandomRatingDistribution();

      this.showDistribution = true;

     
      this.drawRatingChart();
    },
    generateRandomRatingDistribution() {
      const ratingCount = {};
      for (let i = 1; i <= 5; i++) {
        ratingCount[i] = Math.floor(Math.random() * 20) + 1;
      }
      return ratingCount;
    },
    drawRatingChart() {
      const ctx = this.$refs.ratingChart.getContext('2d');

      const data = {
        labels: Object.keys(this.ratingCount).map(Number),
        datasets: [
          {
            label: 'Anzahl der Bewertungen',
            data: Object.values(this.ratingCount),
            backgroundColor: [
              'rgba(255, 99, 132, 0.2)',
              'rgba(255, 159, 64, 0.2)',
              'rgba(255, 205, 86, 0.2)',
              'rgba(75, 192, 192, 0.2)',
              'rgba(54, 162, 235, 0.2)',
            ],
            borderColor: [
              'rgba(255, 99, 132, 1)',
              'rgba(255, 159, 64, 1)',
              'rgba(255, 205, 86, 1)',
              'rgba(75, 192, 192, 1)',
              'rgba(54, 162, 235, 1)',
            ],
            borderWidth: 1,
          },
        ],
      };

      const options = {
        scales: {
          y: {
            beginAtZero: true,
          },
        },
      };

      new Chart(ctx, {
        type: 'bar',
        data: data,
        options: options,
      });
    },
  },
};
</script>

<style scoped>

</style>

  