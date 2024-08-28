<script setup>
import { reactive } from 'vue'

const counter = reactive({ count: 0 });
function meme(){
  counter.count ++;
}


</script>

<template>
  <div @click="meme()">
    This is my GG1.
    {{ counter.count }}
  </div>
</template>