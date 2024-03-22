<template>
  <div id="app">
    <div class="products">
      <h2>Cellphone Shop</h2>
      <div class="product-list">
        <Product v-for="product in products" :key="product.id" :product="product" @add-to-cart="addToCart"></Product>
      </div>
    </div>
    <div class="cart">
      <h2>My Cart</h2>
      <div class="cart-items">
        <CartItem v-for="item in cart" :key="item.id" :item="item" @remove-from-cart="removeFromCart" @update-quantity="updateQuantity"></CartItem>
      </div>
      <p>Total: {{ formatPrice(total) }}</p>
      <button class="checkout-button" @click="checkout">Check Out</button>
    </div>
  </div>
</template>

<script>
import Product from "./components/Product.vue";
import CartItem from "./components/CartItem.vue";

export default {
  components: {
    Product,
    CartItem
  },
  data() {
    return {
      products: [
        { id: 1, name: "OnePlus 9 Pro", price: 61544 },
        { id: 2, name: "Xiaomi Mi 11 Ultra", price: 54000 },
        { id: 3, name: "Sony Xperia 1 III", price: 45000 },
        { id: 4, name: "Samsung Galaxy S21 Ultra", price: 67144 },
        { id: 5, name: "Huawei P50 Pro", price: 46500 },
        { id: 6, name: "iPhone 15 Pro Max ", price: 61544 },
        { id: 7, name: "Asus ROG Phone 5", price: 35000 },
        { id: 8, name: "Google Pixel 6 Pro", price: 50000 },
        { id: 9, name: "Oppo Find X3 Pro", price: 34550 },
        { id: 10, name: "Vivo X70 Pro+", price: 64000 }
      ],
      cart: [],
      total: 0
    };
  },
  methods: {
    addToCart(product) {
      const existingItem = this.cart.find(item => item.id === product.id);
      if (existingItem) {
        existingItem.quantity++;
      } else {
        this.cart.push({ ...product, quantity: 1 });
      }
      this.calculateTotal();
    },
    removeFromCart(item) {
      this.cart = this.cart.filter(cartItem => cartItem.id !== item.id);
      this.calculateTotal();
    },
    updateQuantity({ item, quantity }) {
      const cartItem = this.cart.find(cartItem => cartItem.id === item.id);
      cartItem.quantity = quantity;
      this.calculateTotal();
    },
    calculateTotal() {
      this.total = this.cart.reduce((acc, item) => acc + item.price * item.quantity, 0);
    },
    formatPrice(price) {
      return `₱${price.toLocaleString()}`;
    },
    checkout() {
      if (this.cart.length === 0) {
        alert("Your cart is empty. Please add items before checking out!!");
      } else {
        alert(`Total Price: ${this.formatPrice(this.total)}`);
        this.cart = [];
        this.total = 0;
      }
    }
  }
};
</script>

<style>
body {
  background-color: #00c3ff; 
}

#app {
  display: flex;
  flex-direction: column;
}

.products {
  margin-bottom: 20px;
}

.cart {
  margin-top: auto; 
}

.product-list {
  display: grid;
  grid-template-columns: repeat(5, 1fr);
  gap: 20px;
}

.cart-items {
  display: grid;
  grid-template-columns: repeat(5, 1fr); /* Adjust the number of columns as needed */
  gap: 20px;
}

.product, .cart-item {
  border: 1px solid #026096;
  padding: 10px;
  border-radius: 5px;
  background-color: #f9f9f9b4;
}

.product button, .cart-item button {
  background-color: #4400fd;
  color: white;
  border: none;
  padding: 5px 10px;
  cursor: pointer;
}

.product button:hover, .cart-item button:hover {
  background-color: #b13301;
}

.cart-item {
  margin-bottom: 10px;
}

.cart p {
  font-weight: bold;
}

.checkout-button {
  background-color: #4400fd;
  color: white;
  border: none;
  padding: 5px 10px;
  cursor: pointer;
}

.checkout-button:hover {
  background-color: #b13301;
}
</style>
