<template>
    <div>
         <p>Answer Yes/No question:</p> 
         <input type="text" v-model="question" :disabled="loading">
         <p>{{ answers }}</p>
     </div>
 </template>
 
 <script setup>
     import { ref, watch } from 'vue';
     
     const question = ref("");
     const answers  = ref("Questions usually contain a question mark. ;-)");
     const loading = ref(false);
 
     watch(question, async (newQuestion) => {
         if (newQuestion.includes("?")) {
             loading.value = true;
             answers.value = "Thinking ...";
             try {
                 const response = await fetch('https://yesno.wtf/api');
                 answers.value = (await response.json()).answer;
             } catch (error) {
                 answers.value = 'Error! Could not reach the API. ' + error;
             } finally {
                 loading.value = false;
             }
         }
     });
 </script> 