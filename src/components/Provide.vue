<template>
    <div>Provide Component</div>
  </template>
  
  <script setup>
  import { provide } from 'vue';
  
  const dataToShare = 'Hello from Provide Component';
  console.log('Providing:', dataToShare);
  provide('sharedData', dataToShare);
  </script>