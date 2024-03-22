<template>
  <div class="cart-item">
    <h4>{{ item.name }}</h4>
    <p>{{ formatPrice(item.price) }}</p>
    <input type="number" v-model.number="quantity" @input="updateQuantity">
    <button @click="removeFromCart">Remove</button>
  </div>
</template>

<script>
export default {
  props: {
    item: Object
  },
  data() {
    return {
      quantity: this.item.quantity
    };
  },
  methods: {
    removeFromCart() {
      this.$emit('remove-from-cart', this.item);
    },
    updateQuantity() {
      this.$emit('update-quantity', { item: this.item, quantity: parseInt(this.quantity) });
    },
    formatPrice(price) {
      return `₱${price.toLocaleString()}`;
    }
  }
};
</script>
