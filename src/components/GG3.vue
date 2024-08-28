<script setup>
import { ref } from 'vue';
const styleClass = ref('title');
const myNumber = ref(0);
const increase = ()=> myNumber.value ++;
const myDelay = ()=>{
    setTimeout(increase, 1000)
}
</script>
<template>
    <div>
        <p :class="styleClass">EFFEFEFEFEF</p>
        <p :ref="myDelay">{{ myNumber }}</p>
    </div>
    <div>
        <button class="px-5 py-2 bg-green-500 rounded-md" @click="increase">Click Me</button>
    </div>
</template>
<style>
    .title{
        color:red;
    }
</style>