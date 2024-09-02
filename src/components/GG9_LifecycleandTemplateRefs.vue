<template>
    <!-- Using ref to handling all the DOM updates -->
     <!-- And we can access element use with attribue ref with _nameofRef.value.textContent or so on -->
    <div>
        <p ref="myRef">Hello kon Papa</p>
    </div>
</template>

<script setup>
    import { onMounted, ref } from 'vue';
    const myRef = ref(null);
    myRef.value.textContent = "Hello GG";
    onMounted(()=>{
    });
</script>