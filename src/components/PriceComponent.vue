<template>
  <div class="price-container">
    {{ formattedPrice }}
  </div>
</template>

<script>
export default {
  data() {
    return {
      price: Math.floor(Math.random() * 301), 
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
  color: #e47911; 
  font-weight: bold;
}
</style>

