<script setup>
import { ref } from 'vue';
let me1, me2;
const message = ref('Hello, world!');
console.log(message.value);
me1 = message.value;
message.value='change';
console.log(message.value);
me2 = message.value;
const myFunction = () => message.value = (me1 == message.value) ? me2 : me1;
</script>
<template>
    <div>
        {{ message }}
    </div>
    <button class="px-4 py-2 bg-blue-400 rounded-md" @click="myFunction">Click me</button>
</template>