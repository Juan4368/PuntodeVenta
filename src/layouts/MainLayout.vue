<template>
  <q-layout view="lHh Lpr lFf">
    <q-header elevated>
      <q-toolbar class="q-pa-sm">
        <q-input
          filled
          debounce="300"
          v-model="searchTerm"
          placeholder="Buscar producto por nombre o c\u00f3digo"
          clearable
          class="full-width"
        >
          <template #append>
            <q-icon name="search" />
          </template>
        </q-input>
      </q-toolbar>
    </q-header>

    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script setup lang="ts">
import { searchTerm } from '../stores/search';
</script>
