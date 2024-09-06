<template>
    <div>
      <!-- Bind the ref to the input element -->
      <input type="text" ref="myRef" />
      <!-- Display the value of myLetter -->
      <p>{{ myLetter }}</p>
    </div>
  </template>
  
  <script setup>
  import { onMounted, ref, watch } from 'vue';
  
  // Initialize myRef as null, since it will hold a reference to a DOM element
  const myRef = ref(null);
  // Initialize myLetter to an empty string
  const myLetter = ref("");
  
  // Use onMounted to access the DOM element and set the focus
  onMounted(() => {
    if (myRef.value) {
      // Set the value of myLetter to the current value of the input field
    //   myLetter.value = myRef.textContent;
      // Focus the input field
      console.log(myRef.value);// it return <input type="text"/>
      myRef.value.focus();
    }
  });
  watch(myLetter, (myGG)=>{
    console.log(myGG.value);
  }, {immediate : true})
  </script>
  