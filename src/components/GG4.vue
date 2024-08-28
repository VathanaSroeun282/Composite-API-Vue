<script setup>
    import { ref, reactive } from 'vue';
    const text  = ref('');
    let inputValue = ref('');
    const myMeme = reactive([ref(null), ref(null)]);
    let gg ;
    const handleInput = (e) =>{
        gg = e.target.value;
    }
    const handleClick = () => {
        text.value = gg;
        inputValue.value = "";
    }
    const myArray = reactive([
        {
            id  : 1,
            meme : "Meme1",
            show: false
        },
        {
            id : 2, 
            meme : "Meme2",
            show: false
        }
    ])
    const handleClickMeme = (index) => {
        myMeme[index].value = myArray[index].id;
        myArray.forEach(key => key.show == false);
        myArray[index].show = !myArray[index].show;
    }
</script>
<template>
    <div>
        {{ text }}
    </div>
    <input type="text" v-model="inputValue" @input="handleInput" placeholder="Input here">
    <button @click="handleClick"  class="px-4 py-1 bg-blue-500 rounded-md">
        Click to show your input
    </button>
    <div v-for="(item, index) in myArray" :key="index">
        <button @click="handleClickMeme(index)">
            {{ item.meme }}
        </button>  
        <span v-if="item.show">
            <p>{{ myMeme[index] }}</p>
        </span>
    </div>
</template>