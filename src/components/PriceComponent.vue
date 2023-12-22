<template>
  <div class="price-container">
    {{ formattedPrice }}
  </div>
</template>

<script>
export default {
  data() {
    return {
      price: Math.floor(Math.random() * 301), // Zufälliger Preis zwischen 0 und 300 Fr.
    };
  },
  computed: {
    formattedPrice() {
      return "Aktueller Preis: " + this.price.toFixed(2) + " Fr.";
    },
  },
};
</script>

<style scoped>
.price-container {
  font-size: 16px;
  color: #e47911;
  font-weight: bold;
}
</style>


<style scoped>
.price-container {
  font-size: 16px;
  color: #e47911; /* Beispiel für eine orangefarbene Preisfarbe */
  font-weight: bold;
}
</style>

