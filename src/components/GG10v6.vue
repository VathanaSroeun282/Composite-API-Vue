<template>
    <div class="font-bold text-6xl w-full h-[100vh] bg-green-400 flex justify-center items-center flex-col gap-10">
        <p>{{ myArray.ID }}</p>
        <p>{{ myArray.NAME }}</p>
        <p>{{ myArray.ADDRESS.StreetNumber }}</p>
        <p>{{ count }}</p>
        <p>----------------</p>
        <p>{{ x }}</p>
        <p>{{ y }}</p>
    </div>
</template>

<script setup>
import { reactive, ref, watch, onUnmounted } from 'vue';

const id = ref(0);
const myArray = reactive({
    ID: id.value++,
    NAME: "GGG",
    ADDRESS: {
        Village: "OSVAY",
        Commimune: "PREKUY",
        Province: "KAMPONGCHAM PROVINCE",
        StreetNumber: 12
    }
});
const x = ref(0);
const y = ref(0);
const count = ref(0);

watch(myArray, (myArray) => {
    count.value++;
    console.log(myArray.ADDRESS.StreetNumber);
}, { deep: true });
setInterval(() => {
    myArray.ADDRESS.StreetNumber += 4;
}, 500)

watch(x, newX => console.log("This is new X1 : " + newX));
watch(() => x.value + y.value, sum => console.log("Sum X + Y is : " + sum));
watch([x, () => y.value], ([newX, newY]) => {
    console.log(`X is ${newX}, Y is ${newY}`);
});

</script>
