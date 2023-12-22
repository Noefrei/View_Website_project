<template>
  <div>
    <div v-for="product in products" :key="product.id">
      <Product :data="product" />
      <PriceComponent />
    </div>
  </div>
</template>

<script>
import Product from "./Product.vue";
import PriceComponent from "./PriceComponent.vue";

export default {
  components: {
    Product,
    PriceComponent,
  },

  data() {
    const legoImages = [
      "/Lego Bilder/lego1.jpg",
      "/Lego Bilder/lego2.jpg",
      "/Lego Bilder/lego3.jpg",
      "/Lego Bilder/lego4.jpg",
      "/Lego Bilder/lego5.jpg",
      "/Lego Bilder/lego6.jpg",
      "/Lego Bilder/lego7.jpg",
      "/Lego Bilder/lego8.jpg",
      "/Lego Bilder/lego9.jpg",
      "/Lego Bilder/lego10.jpg",
    ];

    const products = Array.from({ length: 10 }, (_, index) => ({
      id: String(index + 1),
      imageUrl: legoImages[index % legoImages.length],
      productName: `Lego Figure ${index + 1}`,
      releasedDate: "May 31, 2023",
      description: "A cool Lego figure for your collection.",
    }));

    return {
      products,
    };
  },
};
</script>

