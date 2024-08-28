<script setup>
    import { ref } from 'vue';
    let id = 0

    const newTodo = ref('')
    const todos = ref([
    { id: id++, text: 'Learn HTML' },
    { id: id++, text: 'Learn JavaScript' },
    { id: id++, text: 'Learn Vue' }
    ]);
    const addTodo = ()=> {

        todos.value.push({id : id++, text : newTodo.value});
        newTodo.value = '';
    };
    const removeTodo = (item) => {
        todos.value = todos.value.filter((x)=> x !== item);
    };
</script>

<template>
    <form @submit.prevent="addTodo">
        <input v-model="newTodo" required placeholder="new todo">
        <button>Add Todo</button>
    </form>
    <ul>
        <li v-for="(item, index) in todos" :key="index">{{ item.text }}
            <button @click="removeTodo(item)">X</button>
        </li>
    </ul>
</template>