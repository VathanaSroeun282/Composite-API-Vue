<template >
    <div class="font-bold text-6xl w-full h-[100vh] bg-green-400 flex justify-center items-center flex-col gap-10">
        <p>Please Input Answer yes or no !</p>
        <input type="text" class="px-11" :disabled="loading" v-model="question" placeholder="Yes / No">
        <p ref="answer">Hey you! please input question mark in your question?</p>
    </div>
</template>
<script setup>
    import {ref, watch} from 'vue';
    const question = ref("");
    const answer   = ref("");
    const loading  = ref(false);

    // Watch time
    watch(question, async (question)=>{
        if(question.includes('?')){
            answer.value.textContent = "Thinking...";
            loading.value = true;
            try{
                const respon = await fetch('https://yesno.wtf/api');
                answer.value.textContent = (await respon.json()).answer;
            }catch(error){
                answer.value.textContent = "Error! Cloud connot reach the API!";
            }finally{
                loading.value = false;
            }
        }
    })

</script>