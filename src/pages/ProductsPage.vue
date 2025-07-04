<template>
  <q-page class="q-pa-md">
    <q-table
      :rows="products"
      :columns="columns"
      row-key="id"
      flat
    />
  </q-page>
</template>

<script setup lang="ts">
import { ref, onMounted } from 'vue';

type Product = {
  id: number;
  name: string;
  price: number;
};

const products = ref<Product[]>([]);

const columns = [
  { name: 'id', label: 'ID', field: 'id', align: 'left' },
  { name: 'name', label: 'Name', field: 'name', align: 'left' },
  { name: 'price', label: 'Price', field: 'price', align: 'left' }
];

onMounted(async () => {
  try {
    const res = await fetch('/api/products');
    if (res.ok) {
      products.value = await res.json();
    }
  } catch (err) {
    console.error('Failed to load products', err);
  }
});
</script>
