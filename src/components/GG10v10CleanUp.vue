<script setup >
import { ref, watch, effect, onUnmounted, watchEffect } from 'vue';
const data = ref(null);
const apiID = ref(1);
const count = ref(0);
const controller = new AbortController();
const respon = async (id)=>{
    const myRes = await fetch(`https://jsonplaceholder.typicode.com/todos/${id}`)
    data.value = await myRes.json();
    onUnmounted(()=>{
        console.log("Components onUnmounted is cleaning up.");
    });
}
await respon(apiID.value);
// Use onUnmounted

// Cannot use onCleanup as 3rd arguments in call back function in watch because it require vue 3.5+
// Use onUnmounted in watch 
watch(apiID,async (newID, oldID)=>{
    console.log("apiID changed from " , oldID, " to " , newID);
    await respon(newID);
}, {immediate : true});
watch(count, newCount =>{
    console.log("newCount : ",newCount);
}, {immediate :true})
// Use Effect  
effect(()=>{
    console.log("Effect Count : " , count.value);
    return ()=>{
        console.log("Effect Cleanup")
    }
})
// Use AbortController

watch(apiID,async (newID)=>{
    const myRespon = await fetch(`https://jsonplaceholder.typicode.com/todos/${newID}`, {signal : controller.signal});
    data.value = await myRespon.json();
}, {immediate : true});

onUnmounted(()=>{
    controller.abort();
    console.log("Component unmounted. Aborting fetch request.");
});
setInterval(()=>{
    apiID.value ++;
    count.value++;
},5000);

// This lesson mean you avoid the state change before fetch data from api!
</script>
<template>
    <div>
        <h1>Use Watch</h1>
        <p>User iD : {{ data.userId }}</p>
        <p>JUst iD : {{ data.id }}</p>
        <p>Title   : {{ data.title }}</p>
        <p>Completed: {{ data.completed }}</p>
    </div>
</template>