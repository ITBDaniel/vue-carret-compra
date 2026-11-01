<script setup>
import { inject, ref } from 'vue';
import CartItem from './CartItem.vue';

const cart = inject('cart', ref([]));
const totalItems = inject('totalItems', ref(0));
const totalPrice = inject('totalPrice', ref(0));
const clearCart = inject('clearCart', () => {});

const formatPrice = (value) =>
  new Intl.NumberFormat('ca-ES', {
    style: 'currency',
    currency: 'EUR'
  }).format(value);
</script>

<template>
  <aside class="cart-panel">
    <div class="cart-header">
      <h2>Carret</h2>
      <button v-if="cart.length" type="button" class="clear-button" @click="clearCart()">
        🗑️ Buida carret
      </button>
    </div>

    <p class="summary" v-if="totalItems > 0">
      Tens {{ totalItems }} article{{ totalItems === 1 ? '' : 's' }} al carret.
    </p>
    <p class="empty" v-else>El carret està buit.</p>

    <ul class="cart-list" v-if="cart.length">
      <CartItem v-for="item in cart" :key="item.id" :item="item" />
    </ul>

    <div class="total-row" v-if="cart.length">
      <span>Total</span>
      <strong>{{ formatPrice(totalPrice) }}</strong>
    </div>
  </aside>
</template>

<style scoped>
.cart-panel {
  background: rgba(15, 23, 42, 0.97);
  color: #e2e8f0;
  border-radius: 20px;
  padding: 20px;
  position: sticky;
  top: 20px;
  box-shadow: 0 20px 40px rgba(15, 23, 42, 0.22);
}

.cart-header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 12px;
  margin-bottom: 16px;
}

.cart-header h2 {
  margin: 0;
  font-size: 1.6rem;
}

.clear-button {
  border: none;
  background: #ef4444;
  color: white;
  border-radius: 10px;
  padding: 8px 10px;
  font-weight: 700;
  cursor: pointer;
}

.summary,
.empty {
  margin: 0 0 16px;
  color: #cbd5e1;
}

.cart-list {
  margin: 0;
  padding: 0;
}

.total-row {
  margin-top: 18px;
  padding-top: 16px;
  border-top: 1px solid rgba(148, 163, 184, 0.4);
  display: flex;
  justify-content: space-between;
  align-items: center;
  font-size: 1.1rem;
}
</style>
