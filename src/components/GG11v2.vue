<script setup>
import { onMounted, ref } from 'vue'

// the first argument must match the ref value in the template
const inputG = ref(null)

onMounted(() => {
  inputG.value.focus()
})
</script>

<template>
    <p>efwiuefgie</p>
  <input ref="inputG" type="text" class="w-full bg-green-400 h-40"/>
</template>