<template>
    <div>Inject Component: {{ sharedData }}</div>
  </template>
  
  <script setup>
  import { inject } from 'vue';
  
  const sharedData = inject('sharedData', 'Default Value');
  console.log('Injected:', sharedData);
  </script>