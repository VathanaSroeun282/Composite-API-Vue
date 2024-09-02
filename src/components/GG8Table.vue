<script setup>
import { defineProps, defineEmits, ref, computed } from 'vue';

const props = defineProps({
    dataEntries: {
        type: Array,
        required: true
    },
    tableStyle: {
        type: Object,
        required: true
    }
});
const checkAllBox = ref(false);
const checkBox = ref(false);
const emit = defineEmits();

function handleEdit(item) {
    emit('edit', item);  
}

function handleRemove(item) {
    emit('remove', item);
}

const handleHideAndShowItems = computed(() =>
  {
    return checkAllBox.value? '' : (checkBox.value ?  props.dataEntries.filter((x) => !x.done) : props.dataEntries);
  }
);
</script>

<template>
    <div :class="tableStyle.divContainer">
        <table :class="tableStyle.tableContainer">
            <thead class="text-xs text-gray-700 uppercase bg-gray-50 dark:bg-gray-700 dark:text-gray-400">
                <tr>
                    <th scope="col" class="p-4">
                        <div class="flex items-center">
                            <input
                                id="checkbox-all-search"
                                v-model="checkAllBox"
                                type="checkbox"
                                class="w-4 h-4 text-blue-600 bg-gray-100 border-gray-300 rounded focus:ring-blue-500 dark:focus:ring-blue-600 dark:ring-offset-gray-800 dark:focus:ring-offset-gray-800 focus:ring-2 dark:bg-gray-700 dark:border-gray-600"
                            />
                            <label for="checkbox-all-search" class="sr-only">checkbox</label>
                        </div>
                    </th>
                    <th scope="col" class="px-6 py-3">ID</th>
                    <th scope="col" class="px-6 py-3">Name</th>
                    <th scope="col" class="px-6 py-3">Sex</th>
                    <th scope="col" class="px-6 py-3">Address</th>
                    <th scope="col" class="px-6 py-3">Done</th>
                    <th scope="col" class="px-6 py-3">Status</th>
                    <th scope="col" class="px-6 py-3">Action</th>
                </tr>
            </thead>
            <tbody :class="tableStyle.tbodyStyle.tbody">
                <tr
                    v-for="(entry, index) in handleHideAndShowItems"
                    :key="index"
                    :class="tableStyle.tbodyStyle.trStyle"
                >
                    <td :class="tableStyle.checkBoxStyle.tdStyle">
                        <div :class="tableStyle.checkBoxStyle.tdGoDivStyle">
                            <input
                                id="checkbox-table-search"
                                type="checkbox"
                                v-model="entry.done"
                                :class="tableStyle.checkBoxStyle.tdGoDivGoInputCheckBoxStyle"
                            />
                            <label for="checkbox-table-search" :class="tableStyle.checkBoxStyle.tdGoDivGoLabelStyle">checkbox</label>
                        </div>
                    </td>
                    <td :class="tableStyle.tbodyStyle.tdStyle">{{ entry.id }}</td>
                    <td :class="tableStyle.tbodyStyle.tdStyle">{{ entry.name }}</td>
                    <td :class="tableStyle.tbodyStyle.tdStyle">{{ entry.sex }}</td>
                    <td :class="tableStyle.tbodyStyle.tdStyle">{{ entry.address }}</td>
                    <td :class="tableStyle.tbodyStyle.tdStyle">{{ entry.done ? 'Yes' : 'No' }}</td>
                    <td :class="tableStyle.tbodyStyle.tdStyle">{{ entry.status }}</td>
                    <td :class="tableStyle.tbodyStyle.tdStyle">
                        <a
                            href="#"
                            class="font-medium text-blue-600 dark:text-blue-500 hover:underline"
                            @click.prevent="handleEdit(entry)"
                        >
                            Edit
                        </a>
                        <a
                            href="#"
                            :class="tableStyle.tbodyStyle.btnStyle"
                            @click.prevent="handleRemove(entry)"
                        >
                            Remove
                        </a>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    <button @click="checkBox = !checkBox" class="px-8 py-3 bg-blue-400 my-4 rounded-md">
        {{ checkBox ? 'Hide checkBox' : 'Show checkBox' }}
    </button>
</template>
