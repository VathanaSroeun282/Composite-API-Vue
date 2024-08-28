<script setup>
    import { reactive, ref } from 'vue';
    const myGG = ref(true);
    const handleClick = ()=> {
        myGG.value = !myGG.value
    }
    const myText = reactive([
    {
        id : ref(1),
        GG : ref('123') 
    }
    ]);
</script>
<template >
    <div>
        <button class="px-5 py-2 bg-blue-400 font-bold rounded-md" @click="handleClick">Toggle</button>
        <p v-if="myGG">
            <span v-for="(item, index) in myText" :key="index">{{ item.id + item.GG }}</span>
        </p>
    </div>
</template>