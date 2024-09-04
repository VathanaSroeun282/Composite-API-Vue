<template>
    <div>
       <p>{{ myResult }}</p> 
    </div>
</template>
<script setup>
import { ref, watch } from 'vue';
let count = ref (0);
let myResult = ref ('');
watch (count,(newValue, oldValue)=>{
    console.log(`This is a Old Value : ${oldValue} \nThis is a New Value : ${newValue}`);
    myResult.value = "New Value : " + newValue + " OldValue : " + oldValue;
}, {immediate: true, once :true});

setInterval(()=>{
    count.value++;
}, 400);
</script>