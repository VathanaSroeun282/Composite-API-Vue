<template>
    <div>
        <div>
            <h1>This is use with watch function</h1>
            <p>{{ todo }}</p>
            <!-- <div>{{ data }}</div> -->
            <p>User ID: {{ data.userId }}</p>
            <p>ID: {{ data.id }}</p>
            <p>Title: {{ data.title }}</p>
            <p>Completed: {{ data.completed }}</p>
        </div>
        <p>-----------------------------------------------</p>
        <div>
            <h1>This is use with watchEffect function</h1>
            <p>{{ todo }}</p>
            <!-- <div>{{ data }}</div> -->
            <p>User ID: {{ mYdata.userId }}</p>
            <p>ID: {{ mYdata.id }}</p>
            <p>Title: {{ mYdata.title }}</p>
            <p>Completed: {{ mYdata.completed }}</p>
        </div>
    </div>
</template>

<script setup>
import { ref, watch, watchEffect } from 'vue';

const todo = ref(1);
const data = ref(null);
const mYdata = ref(null);

// Watch the `todo` value and fetch new data when it changes
watch(todo, async (newValue) => {
    try {
        const response = await fetch(`https://jsonplaceholder.typicode.com/todos/${newValue}`);
        if (!response.ok) {
            throw new Error('Network response was not ok');
        }
        data.value = await (response.json());
        console.log(data)
    } catch (error) {
        console.error('Fetch error:', error);
        data.value = null; // Handle errors by setting data to null
    }
}, { immediate: true });
watchEffect(async ()=>{
    try{
        const response = await fetch(`https://jsonplaceholder.typicode.com/todos/${todo.value}`);
        if(!response.ok){
            throw new Error("This api cannot fetch properly");
        }
        mYdata.value = await response.json();
    }
    catch(error){
        console.error('Errors : ', error);
    }
})
//   Increment the   `todo` value every second
setInterval(() => {
    todo.value++;
}, 1000);
</script>