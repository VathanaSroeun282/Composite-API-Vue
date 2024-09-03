<template>
    <div>
        <p>Please just put yes/no answers : </p>
        <input type="text" v-model="question" :disabled="loading" name="name" placeholder="yes/no">
        <p>{{ answer }}</p>
    </div>
</template>
<script setup>
    import { ref, watch } from 'vue';
    const answer = ref("Question always contains question mark ? :)");
    const question = ref("");
    const loading  = ref(false);
    watch(question, async (question)=>{
        if(question.includes('?')){
            loading.value = true;
            answer.value  = "Thinking...";
            try{
                const respon = await fetch('https://yesno.wtf/api');
                answer.value = (await respon.json()).answer;
            }
            catch(error){
                answer.value += "Error! Cloud not reach The API!";
            }
            finally {
                loading.value = false;
            }
        }
    })
</script>
 