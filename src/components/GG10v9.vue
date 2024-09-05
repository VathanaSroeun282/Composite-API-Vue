<script setup>
import { ref, watch, watchEffect } from 'vue';
    const apiID = ref(1);
    const datas = ref(null);
    const myDatas = ref(null);
    watch(apiID, async (newID)=>{
        const respon = await fetch(`https://jsonplaceholder.typicode.com/todos/${newID}`);
        datas.value = await respon.json();
    }, {immediate : true});

    watchEffect(async ()=>{
        const respon = await fetch(`https://jsonplaceholder.typicode.com/todos/${apiID.value}`);
        myDatas.value  = await respon.json();
    });
    setInterval(()=>{
        apiID.value ++;
    }, 500);
</script>
<template>
    <div>
        <h1>Use Watch</h1>
        <p>User iD : {{ datas.userId }}</p>
        <p>JUst iD : {{ datas.id }}</p>
        <p>Title   : {{ datas.title }}</p>
        <p>Completed: {{ datas.completed }}</p>
    </div>
    <hr class="h-4 bg-black">
    <div>
        <h1>Use watchEffect</h1>
        <p>User iD : {{ myDatas.userId }}</p>
        <p>JUst iD : {{ myDatas.id }}</p>
        <p>Title   : {{ myDatas.title }}</p>
        <p>Completed: {{ myDatas.completed }}</p>
    </div>
</template>