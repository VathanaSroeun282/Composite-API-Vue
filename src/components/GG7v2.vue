<script setup>
import {computed, handleError, ref} from 'vue';
    let id = 0;
    const newData = ref('');
    const boxCheck = ref(false);
    const datas = ref([
        {
            id : id ++, 
            name : 'Kaka',
            Sex  : 'Male',
            done : false
        },
        {
            id : id ++, 
            name : 'Kimkim',
            Sex  : 'Female',
            done : false
        },
        {
            id : id ++, 
            name : 'Kak kak',
            Sex  : 'Male',
            done : true
        }
    ])
    const handleDelete  = (itemID)=>{
        datas.value = datas.value.filter(x=>x!==itemID)
    }
    const handleSubmit = ()=>{
        datas.value.push({id: id++, name : newData, Sex : 'None', done : false});
    }
    const hideDataCheck = computed(()=>{
        return boxCheck.value ? (datas.value.filter((x)=>!x.done)) : datas.value;
    });
</script>
<template>
    <div>
        <form @submit.prevent="handleSubmit">
            <input type="text" v-model="newData" placeholder="Enter your name">
            <button type="submit">submit</button>
        </form>
        <ul>
            <li v-for="(item, index) in hideDataCheck" :key="index">
                {{ item.id }}
                {{ item.name }}
                {{ item.Sex }} 
                <span></span>
                <input type="checkbox" v-model="item.done">
                <button @click="handleDelete(item)">Delete</button>
            </li><br>
        </ul>
        <button @click="boxCheck =!boxCheck">{{ boxCheck?'Hide':'Show' }}</button>
    </div>
</template>