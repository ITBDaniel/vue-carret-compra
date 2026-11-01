<script setup>
import { computed, provide, ref } from 'vue';
import CategoryList from './components/CategoryList.vue';
import Cart from './components/Cart.vue';

const products = ref([
  {
    id: 1,
    name: 'Auriculars X10',
    category: 'Audio',
    price: 79.99,
    description: 'So de qualitat i cancel·lació de soroll.'
  },
  {
    id: 2,
    name: 'Smartwatch Pro',
    category: 'Wearables',
    price: 159.0,
    description: 'Monitoratge esportiu i notificacions intel·ligents.'
  },
  {
    id: 3,
    name: 'Teclat Mecànic K2',
    category: 'Perifèrics',
    price: 129.5,
    description: 'Switches clars i disseny ultra compacte.'
  },
  {
    id: 4,
    name: 'Altaveu Bluetooth Mini',
    category: 'Audio',
    price: 54.9,
    description: 'Portàtil, potent i ideal per viatjar.'
  },
  {
    id: 5,
    name: 'Rellotge Fit Max',
    category: 'Wearables',
    price: 99.0,
    description: 'Seguiment del son, passos i ritme cardíac.'
  },
  {
    id: 6,
    name: 'Ratolí Ergonòmic M7',
    category: 'Perifèrics',
    price: 69.99,
    description: 'Precisió i comoditat per llargues jornades.'
  }
]);

const cart = ref([]);

const addToCart = (product) => {
  const existingItem = cart.value.find((item) => item.id === product.id);

  if (existingItem) {
    existingItem.quantity += 1;
    return;
  }

  cart.value.push({ ...product, quantity: 1 });
};

const removeFromCart = (productId) => {
  cart.value = cart.value.filter((item) => item.id !== productId);
};

const clearCart = () => {
  cart.value = [];
};

const totalItems = computed(() =>
  cart.value.reduce((sum, item) => sum + item.quantity, 0)
);

const totalPrice = computed(() =>
  cart.value.reduce((sum, item) => sum + item.quantity * item.price, 0)
);

provide('products', products);
provide('cart', cart);
provide('addToCart', addToCart);
provide('removeFromCart', removeFromCart);
provide('clearCart', clearCart);
provide('totalItems', totalItems);
provide('totalPrice', totalPrice);
</script>

<template>
  <main class="shop-page">
    <header class="shop-header">
      <div>
        <p class="eyebrow">Tech Store</p>
        <h1>Botiga de Gadgets</h1>
      </div>
      <div class="cart-badge">
        <span>{{ totalItems }}</span>
        articles
      </div>
    </header>

    <section class="shop-layout">
      <CategoryList />
      <Cart />
    </section>
  </main>
</template>

<style scoped>
:global(body) {
  margin: 0;
  font-family: 'Segoe UI', sans-serif;
  background: linear-gradient(135deg, #f3f4f6 0%, #e0f2fe 100%);
  color: #0f172a;
}

* {
  box-sizing: border-box;
}

.shop-page {
  max-width: 1200px;
  margin: 0 auto;
  padding: 32px 20px 48px;
}

.shop-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 24px;
  gap: 16px;
}

.eyebrow {
  margin: 0;
  text-transform: uppercase;
  font-size: 0.8rem;
  letter-spacing: 0.12em;
  color: #2563eb;
  font-weight: 700;
}

h1 {
  margin: 8px 0 0;
  font-size: clamp(2rem, 5vw, 3rem);
}

.cart-badge {
  background: #0f172a;
  color: #f8fafc;
  padding: 10px 16px;
  border-radius: 999px;
  font-size: 0.9rem;
  display: flex;
  align-items: center;
  gap: 8px;
}

.cart-badge span {
  font-size: 1.2rem;
  font-weight: 700;
}

.shop-layout {
  display: grid;
  grid-template-columns: minmax(0, 2fr) minmax(300px, 1fr);
  gap: 24px;
  align-items: start;
}

@media (max-width: 860px) {
  .shop-layout {
    grid-template-columns: 1fr;
  }

  .shop-header {
    flex-direction: column;
    align-items: flex-start;
  }
}
</style>
