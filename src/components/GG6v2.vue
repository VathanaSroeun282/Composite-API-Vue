<script setup>
import { ref } from "vue";
let id = 0;
const newData = ref('');
const datas = ref([
  {
    id: ++id,
    name: "GG",
    status: "single",
  },
  {
    id: ++id,
    name: "GGG",
    status: "single2",
  },
  {
    id: ++id,
    name: "GG",
    status: "single3",
  },
]);

const handleAdd = ()=>{
    datas.value.push({id : id++, name : newData.value, status: 'single'});
}
const handleDelete = (dataIndexOrKey)=> {
    datas.value = datas.value.filter(x => x.id!==dataIndexOrKey)
}
</script>
<template>
  <form @submit.prevent="handleAdd">
    <input type="text" v-model="newData" placeholder="Enter your name">
    <button>Add Data</button>
  </form>
  <div>
    <table class="border w-[50%]">
        <tr class="border" v-for="(item, index) in datas" :key="index">
            <td class="border border-black">{{ item.id }}</td>
            <td class="border border-black">{{ item.name }}</td>
            <td class="border border-black">{{ item.status }}</td>
            <td class="border border-black"><button @click="handleDelete(item.id)">Delete</button></td>
        </tr>
    </table>
  </div>
</template>
