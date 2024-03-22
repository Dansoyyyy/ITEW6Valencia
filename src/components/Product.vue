<template>
  <div class="product">
    <h3>{{ product.name }}</h3>
    <p>{{ product.price }}</p>
    <button @click="addToCart">Add to Cart</button>
  </div>
</template>

<script>
export default {
  name: 'ProductItem', 
  props: {
    product: Object
  },
  methods: {
    addToCart() {
      this.$emit('add-to-cart', this.product);
    }
  }
};
</script>
