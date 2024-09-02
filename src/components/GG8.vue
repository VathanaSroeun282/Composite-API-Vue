<script setup>
import { reactive, ref } from "vue";
import GG8Table from "./GG8Table.vue";

let id = 1;

const dataDetail = reactive({
  id : "",
  name: "",
  sex: "",
  address: "",
  done: false,
  status: "",
});

const dataBase = ref([
  {
    id: id++,
    name: "John Doe",
    sex: "Male",
    address: "123 Main St",
    done: true,
    status: "Active",
  },
  {
    id: id++,
    name: "Jane Smith",
    sex: "Female",
    address: "456 Oak Ave",
    done: false,
    status: "Inactive",
  },
  {
    id: id++,
    name: "Mike Johnson",
    sex: "Male",
    address: "789 Pine Rd",
    done: true,
    status: "Pending",
  },
  {
    id: id++,
    name: "Emily Brown",
    sex: "Female",
    address: "321 Maple Dr",
    done: false,
    status: "Active",
  },
  {
    id: id++,
    name: "Chris Green",
    sex: "Male",
    address: "654 Elm St",
    done: true,
    status: "Inactive",
  },
  {
    id: id++,
    name: "Anna White",
    sex: "Female",
    address: "987 Cedar Ln",
    done: false,
    status: "Pending",
  },
  {
    id: id++,
    name: "Tom Harris",
    sex: "Male",
    address: "246 Birch Blvd",
    done: true,
    status: "Active",
  },
  {
    id: id++,
    name: "Laura Davis",
    sex: "Female",
    address: "135 Spruce Cir",
    done: false,
    status: "Inactive",
  },
  {
    id: id++,
    name: "Steve Wilson",
    sex: "Male",
    address: "579 Fir Ct",
    done: true,
    status: "Pending",
  },
  {
    id: id++,
    name: "Rachel Lee",
    sex: "Female",
    address: "864 Willow Dr",
    done: false,
    status: "Active",
  },
]);

const formStyle = {
  formClass: "w-[50%] mx-auto bg-gray-400 py-2 px-10",
  divContainer: "mb-5",
  divContainerGoLabel: "block mb-2 text-sm font-medium text-gray-900 dark:text-white",
  divContainerGoInputText: "bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500",
  divContainerGoInputCheckBox: "w-4 h-4 border border-gray-300 rounded bg-gray-50 focus:ring-3 focus:ring-blue-300 dark:bg-gray-700 dark:border-gray-600 dark:focus:ring-blue-600 dark:ring-offset-gray-800 dark:focus:ring-offset-gray-800",
  divContainerGoBtn: "text-white bg-blue-700 hover:bg-blue-800 focus:ring-4 focus:outline-none focus:ring-blue-300 font-medium rounded-lg text-sm w-full sm:w-auto px-5 py-2.5 text-center dark:bg-blue-600 dark:hover:bg-blue-700 dark:focus:ring-blue-800"
};

const tableStyle = {
  divContainer: "relative overflow-x-auto shadow-md sm:rounded-lg",
  tableContainer: "w-full text-sm text-left rtl:text-right text-gray-500 dark:text-gray-400",
  theadStyle: {
    thead: "text-xs text-gray-700 uppercase bg-gray-50 dark:bg-gray-700 dark:text-gray-400",
    trStyle: '',
    thStyle: ['px-6 py-3', 'col']
  },
  tbodyStyle: {
    tbody: '',
    trStyle: 'bg-white border-b dark:bg-gray-800 dark:border-gray-700',
    thStyle: ["row", "px-6 py-4 font-medium text-gray-900 whitespace-nowrap dark:text-white"],
    tdStyle: "px-6 py-4",
    btnStyle: "font-medium text-red-600 dark:text-red-500 hover:underline"
  },
  checkBoxStyle: {
    tdStyle: "w-4 p-4",
    tdGoDivStyle: "flex items-center",
    tdGoDivGoInputCheckBoxStyle: "w-4 h-4 text-blue-600 bg-gray-100 border-gray-300 rounded focus:ring-blue-500 dark:focus:ring-blue-600 dark:ring-offset-gray-800 dark:focus:ring-offset-gray-800 focus:ring-2 dark:bg-gray-700 dark:border-gray-600",
    tdGoDivGoLabelStyle: "sr-only"
  }
};
// Events
const handleDelete = (item) => {
  dataBase.value = dataBase.value.filter(x => x !== item);
};
const handleSubmit = () => { 
 if(dataBase.value.find(x=>x.id === dataDetail.id)){
  dataDetail.id = dataBase.value.length + 1;
  dataBase.value.push({...dataDetail});
  console.log(dataBase.value.length);
 }else
 dataBase.value.push({...dataDetail});
};
const handleEdit = (items) => {
  Object.assign(dataDetail, items);
};
</script>

<template>
  <form :class="formStyle.formClass" @submit.prevent="handleSubmit">
    <div :class="formStyle.divContainer">
      <label :class="formStyle.divContainerGoLabel" for="name">Your ID :</label>
      <input v-model="dataDetail.id" :class="formStyle.divContainerGoInputText" type="text" />
    </div>
    <div :class="formStyle.divContainer">
      <label :class="formStyle.divContainerGoLabel" for="name">Enter Name :</label>
      <input v-model="dataDetail.name" :class="formStyle.divContainerGoInputText" type="text" />
    </div>
    <div :class="formStyle.divContainer">
      <label :class="formStyle.divContainerGoLabel" for="sex">Enter Gender :</label>
      <input v-model="dataDetail.sex" :class="formStyle.divContainerGoInputText" type="text" />
    </div>
    <div :class="formStyle.divContainer">
      <label :class="formStyle.divContainerGoLabel" for="address">Enter Address :</label>
      <input v-model="dataDetail.address" :class="formStyle.divContainerGoInputText" type="text" />
    </div>
    <div :class="formStyle.divContainer">
      <label :class="formStyle.divContainerGoLabel" for="done">done? :</label>
      <input v-model="dataDetail.done" :class="formStyle.divContainerGoInputCheckBox" type="checkbox" />
    </div>
    <div :class="formStyle.divContainer">
      <label :class="formStyle.divContainerGoLabel" for="status">Status:</label>
      <input v-model="dataDetail.status" :class="formStyle.divContainerGoInputText" type="text" />
    </div>
    <div>
      <button :class="formStyle.divContainerGoBtn" type="submit">Add</button>
    </div>
  </form>

  <GG8Table 
    @remove="handleDelete" 
    @edit="handleEdit"
    :dataEntries="dataBase" 
    :tableStyle="tableStyle" 
  />
</template>
