<script setup>
import { ref, watch, watchEffect } from 'vue';
const count = ref(0);
setTimeout(() => {
    watch(count, newCount => {
        console.log("THis is in watch function : ", newCount);
    }, { flush: 'pre' });
    watchEffect(() => {
        console.log("This is data of count  : ", count.value);
    }, { flush: 'pre' })
    setInterval(() => {
        count.value++;
    }, 1000);
}, 5000)
</script>
<template>
    <div>
        <p>Flus : pre or post and </p>
        <p>Hello world</p>
        <p>{{ count }}</p>
    </div>
</template>