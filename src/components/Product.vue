<template>
  <div class="card mb-3">
    <div class="row no-gutters">
      <div class="col-md-4">
        <img :src="data.imageUrl" class="card-img" alt="Lego Figure" />
      </div>
      <div class="col-md-8">
        <div class="card-body">
          <h5 class="card-title">{{ data.productName }}</h5>
          <Rating :initialRating="data.rating" />
          <p class="card-text">{{ data.description }}</p>
          <PriceComponent :price="data.price" />
          <p class="card-text">
            <small class="text-muted">{{ data.releasedDate }}</small>
          </p>
          <button @click="addToCart" class="btn btn-primary">Add to Cart</button>
          <ShoppingCart :cart-items="cartItems" />

          <!-- Integriere die RatingDistribution-Komponente hier -->
          <RatingDistribution :ratings="data.ratings" />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import ShoppingCart from "./ShoppingCart.vue";
import PriceComponent from "./PriceComponent.vue";
import Rating from "./Rating.vue";
import RatingDistribution from "./RatingDistribution.vue"; // Importiere die neue Komponente

export default {
  components: {
    ShoppingCart,
    PriceComponent,
    Rating,
    RatingDistribution, // Füge die neue Komponente zu den Imports hinzu
  },
  props: {
    data: Object,
  },
  data() {
    return {
      cartItems: [],
    };
  },
  methods: {
    addToCart() {
      this.$emit("add-to-cart", this.data);
    },
  },
};
</script>

<style scoped>
.card-img {
  width: 100%;
  height: 100%;
  object-fit: contain; 
}
</style>
