<script setup>
import { inject } from 'vue';

const props = defineProps({
  product: {
    type: Object,
    required: true
  }
});

const addToCart = inject('addToCart', () => {});

const formatPrice = (value) =>
  new Intl.NumberFormat('ca-ES', {
    style: 'currency',
    currency: 'EUR'
  }).format(value);
</script>

<template>
  <article class="product-card">
    <div class="product-badge">{{ product.category }}</div>
    <h3>{{ product.name }}</h3>
    <p>{{ product.description }}</p>
    <div class="product-footer">
      <strong>{{ formatPrice(product.price) }}</strong>
      <button type="button" @click="addToCart(product)">Afegir al carret</button>
    </div>
  </article>
</template>

<style scoped>
.product-card {
  background: #f8fafc;
  border: 1px solid #dbeafe;
  border-radius: 16px;
  padding: 18px;
  display: flex;
  flex-direction: column;
  gap: 12px;
  min-height: 200px;
}

.product-badge {
  width: fit-content;
  background: #dbeafe;
  color: #1d4ed8;
  border-radius: 999px;
  padding: 4px 10px;
  font-size: 0.75rem;
  font-weight: 700;
}

.product-card h3 {
  margin: 0;
  font-size: 1.26rem;
}

.product-card p {
  margin: 0;
  color: #475569;
  line-height: 1.5;
  flex: 1;
}

.product-footer {
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 12px;
}

.product-footer strong {
  font-size: 1.2rem;
}

button {
  border: none;
  border-radius: 10px;
  background: linear-gradient(135deg, #2563eb 0%, #1d4ed8 100%);
  color: white;
  font-weight: 600;
  padding: 10px 14px;
  cursor: pointer;
  transition: transform 0.15s ease, box-shadow 0.15s ease;
}

button:hover {
  transform: translateY(-1px);
  box-shadow: 0 10px 15px rgba(37, 99, 235, 0.2);
}
</style>
