<script setup>
import { computed, inject, ref } from 'vue';
import ProductItem from './ProductItem.vue';

const products = inject('products', ref([]));

const categories = computed(() => {
  const groupedProducts = products.value.reduce((groups, product) => {
    const key = product.category;
    if (!groups[key]) {
      groups[key] = [];
    }

    groups[key].push(product);
    return groups;
  }, {});

  return Object.entries(groupedProducts).map(([name, items]) => ({
    name,
    items
  }));
});
</script>

<template>
  <section class="category-list">
    <div v-for="category in categories" :key="category.name" class="category-block">
      <h2>{{ category.name }}</h2>
      <div class="product-grid">
        <ProductItem v-for="product in category.items" :key="product.id" :product="product" />
      </div>
    </div>
  </section>
</template>

<style scoped>
.category-list {
  display: flex;
  flex-direction: column;
  gap: 24px;
}

.category-block {
  background: rgba(255, 255, 255, 0.8);
  border: 1px solid #e2e8f0;
  border-radius: 18px;
  padding: 20px;
  box-shadow: 0 10px 25px rgba(15, 23, 42, 0.05);
}

.category-block h2 {
  margin: 0 0 18px;
  font-size: 1.4rem;
}

.product-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
  gap: 18px;
}
</style>
