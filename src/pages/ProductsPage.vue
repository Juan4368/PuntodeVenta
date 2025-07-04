<template>
  <q-page class="q-pa-md">
    <q-table :rows="filteredProducts" :columns="columns" row-key="id" flat />
  </q-page>
</template>

<script setup lang="ts">
import { ref, onMounted, computed } from 'vue';
import { searchTerm } from '../stores/search';

type Product = {
  id: number;
  name: string;
  barcode: string;
  price: number;
};

const products = ref<Product[]>([]);

const sampleProducts: Product[] = [
  { id: 1, name: 'Coca Cola', barcode: '1234567890123', price: 1.5 },
  { id: 2, name: 'Pepsi', barcode: '2345678901234', price: 1.4 },
  { id: 3, name: 'Agua', barcode: '3456789012345', price: 0.8 },
];

const columns = [
  { name: 'id', label: 'ID', field: 'id', align: 'left' },
  { name: 'name', label: 'Name', field: 'name', align: 'left' },
  { name: 'barcode', label: 'Barcode', field: 'barcode', align: 'left' },
  { name: 'price', label: 'Price', field: 'price', align: 'left' },
];

onMounted(async () => {
  try {
    const res = await fetch('/api/products');
    if (res.ok) {
      products.value = await res.json();
    } else {
      products.value = sampleProducts;
    }
  } catch (err) {
    console.error('Failed to load products', err);
    products.value = sampleProducts;
  }
});

const filteredProducts = computed(() => {
  if (!searchTerm.value) {
    return products.value;
  }
  const term = searchTerm.value.toLowerCase();
  return products.value.filter(
    (p) => p.name.toLowerCase().includes(term) || p.barcode.toLowerCase().includes(term),
  );
});
</script>
