<script setup>
const props = defineProps({
  item: {
    type: Object,
    required: true
  }
});

const formatPrice = (value) =>
  new Intl.NumberFormat('ca-ES', {
    style: 'currency',
    currency: 'EUR'
  }).format(value);
</script>

<template>
  <li class="cart-item">
    <div>
      <h4>{{ item.name }}</h4>
      <p>{{ item.quantity }} × {{ formatPrice(item.price) }}</p>
    </div>
    <strong>{{ formatPrice(item.quantity * item.price) }}</strong>
  </li>
</template>

<style scoped>
.cart-item {
  list-style: none;
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 12px;
  padding: 12px 0;
  border-bottom: 1px solid #e2e8f0;
}

.cart-item h4 {
  margin: 0 0 4px;
  font-size: 1rem;
}

.cart-item p {
  margin: 0;
  color: #475569;
  font-size: 0.9rem;
}

.cart-item strong {
  font-size: 1rem;
}
</style>
