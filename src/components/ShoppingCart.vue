<template>
    <div class="shopping-cart">
      <h2>Shopping Cart</h2>
      <ul>
        <li v-for="(item, index) in cartItems" :key="index">
          {{ item.name }} - {{ item.price.toFixed(2) }} Fr.
          <button @click="removeFromCart(index)">Remove</button>
        </li>
      </ul>
      <p>Total: {{ calculateTotal().toFixed(2) }} Fr.</p>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        cartItems: [], // Array für die Artikel im Einkaufswagen
      };
    },
    methods: {
      addToCart(item) {
        this.cartItems.push(item);
      },
      removeFromCart(index) {
        this.cartItems.splice(index, 1);
      },
      calculateTotal() {
        return this.cartItems.reduce((total, item) => total + item.price, 0);
      },
    },
  };
  </script>
  
  <style scoped>
  .shopping-cart {
    border: 1px solid #ddd;
    padding: 10px;
    margin: 10px;
  }
  
  ul {
    list-style-type: none;
    padding: 0;
  }
  
  li {
    margin-bottom: 10px;
  }
  </style>
  