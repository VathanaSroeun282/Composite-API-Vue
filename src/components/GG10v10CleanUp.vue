<script setup>
import { ref, watch, onUnmounted, watchEffect } from 'vue';

const data = ref(null);
const apiID = ref(1);
const count = ref(0);
const controller = new AbortController();

const fetchData = async (id) => {
    try {
        const response = await fetch(`https://jsonplaceholder.typicode.com/todos/${id}`, { signal: controller.signal });
        if (!response.ok) throw new Error('Network response was not ok');
        data.value = await response.json();
    } catch (error) {
        if (error.name === 'AbortError') {
            console.log('Fetch aborted');
        } else {
            console.error('Fetch error:', error);
        }e
    }
};

// Initial fetch
await fetchData(apiID.value);

// Watch for changes in apiID
watch(apiID, async (newID, oldID) => {
    console.log("apiID changed from", oldID, "to", newID);
    await fetchData(newID);
}, { immediate: true });

// Watch for changes in count
watch(count, (newCount) => {
    console.log("newCount:", newCount);
}, { immediate: true });

// Use watchEffect for reactive side effects
watchEffect(() => {
    console.log("Effect Count:", count.value);
    // Cleanup logic (optional, but better with watchEffect)
    // cleanup logic here if needed
});

// Periodically update apiID and count
setInterval(() => {
    apiID.value++;
    count.value++;
}, 5000);

// Cleanup on unmount
onUnmounted(() => {
    controller.abort();
    console.log("Component unmounted. Aborting fetch request.");
});
</script>

<template>
    <div class="w-full bg-slate-900 h-[10rem]">
        <h1>Use Watch</h1>
        <p>User iD: {{ data?.userId }}</p>
        <p>Just iD: {{ data?.id }}</p>
        <p>Title: {{ data?.title }}</p>
        <p>Completed: {{ data?.completed }}</p>
    </div>
</template>
