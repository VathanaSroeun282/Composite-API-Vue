<template>
    <div>
        <p>{{ x }}</p>   
        <p>{{ y }}</p>
        <p>{{ mYobject.count }}</p>
    </div>
</template>
<script setup>
import { reactive, ref, watch } from 'vue';
    let x = ref(0);
    let y = ref(0);
    let mYobject  = reactive({count : 0})
    watch(x,(newX)=>{
        console.log("This is new X = "+newX);
    })
    watch(y, newY=>console.log("This is new Y = " + newY));
    // Getter
    watch(()=>x.value + y.value, sum=>console.log("Sum X + Y = " + sum));

    // array of mutiple sources
    watch([x, ()=> y.value],([newX, newY])=> console.log("X is : " + newX + " Y is : " + newY));
    
    // watch cannot observe this object because you are passing value in the watch()
    watch(mYobject.count, (newObj)=>console.log("This is new value of Object" + newObj));

    // to handle this, you have to use arrow function instead
    watch(()=> mYobject.count, newObj => console.log("This is new value of Object" + newObj));
</script>