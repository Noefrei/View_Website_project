<script>
import Product from "./Product.vue";

export default {
  components: {
    Product,
  },
  data() {
    return {
      products: Array.from({ length: 10 }, (_, index) => ({
        id: String(index + 1),
        imageUrl: `https://loremflickr.com/150/150?random=${index + 1}`,
        productName: `Product ${index + 1}`,
        releasedDate: "May 31, 2023", // Du könntest dies auch dynamisch generieren, wenn nötig
        description: "Lorem ipsum dolor sit amet, consectetur...",
        rating: Math.floor(Math.random() * 5) + 1, // Zufällige Bewertung zwischen 1 und 5
      })),
    };
  },
};
</script>

<template>
  <div v-for="product in products" :key="product.id">
    <Product :data="product" />
  </div>
</template>
