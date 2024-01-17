<script setup>
import { ref } from 'vue';

const tasks = ref([
  { name: 'Task 1', time: 30 },
  { name: 'Task 2', time: 40 },
  { name: 'Task 3', time: 60 },
  { name: 'Task 4', time: 45 },
  { name: 'Task 5', time: 50 },
]);

const isEditFormVisible = ref(false);
const editTask = ref({ name: '', time: 0 });
let editIndex = ref(null);

const openEditForm = (index) => {
  editTask.value = { ...tasks.value[index] };
  editIndex.value = index;
  isEditFormVisible.value = true;
};

const updateTask = () => {
  if (editIndex.value !== null) {
    tasks.value[editIndex.value] = { ...editTask.value };
    closeEditForm();
  }
};

const closeEditForm = () => {
  isEditFormVisible.value = false;
  editIndex.value = null;
};
</script>


<template>
  <section>
<div class="relative overflow-x-auto shadow-md sm:rounded-lg">
    <table class="w-full text-sm text-left rtl:text-right text-gray-500 dark:text-gray-400">
        <thead class="text-xs text-gray-700 uppercase bg-gray-50 dark:bg-gray-700 dark:text-gray-400">
            <tr>
                <th scope="col" class="px-6 py-3">
                    Sl/No
                </th>
                <th scope="col" class="px-6 py-3">
                    Task Name
                </th>
                <th scope="col" class="px-6 py-3">
                    Time
                </th>
                <th scope="col" class="px-6 py-3">
                    Action
                </th>
            </tr>
        </thead>
        <tbody>
            <tr class="bg-white border-b dark:bg-gray-800 dark:border-gray-700" v-for="(task, index) in tasks" :key="index">
                <th scope="row" class="px-6 py-4 font-medium text-gray-900 whitespace-nowrap dark:text-white">
                    {{ index+1 }}
                </th>
                <td class="px-6 py-4">
                    {{ task.name }}
                </td>
                <td class="px-6 py-4">
                    {{ task.time }} Minutes
                </td>

                <td class="px-6 py-4">
                  <button class="focus:outline-none text-white bg-red-700 hover:bg-red-800 focus:ring-4 focus:ring-red-300 font-medium rounded-lg text-sm px-5 py-2.5 me-2 mb-2 dark:bg-red-600 dark:hover:bg-red-700 dark:focus:ring-red-900" @click="openEditForm(index)">Edit</button>
                </td>
            </tr>
        </tbody>
    </table>
</div>
</section>
<!-- Modal -->
<div class="fixed z-10 overflow-y-auto top-0 w-full left-0 popup" v-if="isEditFormVisible">
  <form @submit.prevent="updateTask">
  <div class="flex items-center justify-center min-height-100vh pt-4 px-4 pb-20 text-center sm:block sm:p-0">
    <div class="fixed inset-0 transition-opacity">
      <div class="absolute inset-0 bg-gray-900 opacity-75" />
    </div>
    <span class="hidden sm:inline-block sm:align-middle sm:h-screen">&#8203;</span>
    <div class="inline-block align-center bg-white rounded-lg text-left overflow-hidden shadow-xl transform transition-all sm:my-8 sm:align-middle sm:max-w-lg sm:w-full" role="dialog" aria-modal="true" aria-labelledby="modal-headline">
      <div class="bg-white px-4 pt-5 pb-4 sm:p-6 sm:pb-4">
        <label for="editName" class="font-medium text-gray-800">Task Name</label>
        <input id="editName" v-model="editTask.name" type="text" class="text-black w-full rounded bg-gray-100 p-2 mt-2 mb-3">
        <label for="taskTime" class="font-medium text-gray-800">Task Time</label>
        <input id="editTime" v-model="editTask.time" type="number" class="text-black w-full rounded bg-gray-100 p-2 mt-2 mb-3" />
      </div>
      <div class="bg-gray-200 px-4 py-3 text-right">
        <button type="submit" class="py-2 px-4 bg-blue-500 text-white rounded font-medium hover:bg-blue-700 mr-2 transition duration-500"><i class="fas fa-plus"></i> Update </button>
      </div>
    </div>
  </div>
</form>
</div>
</template>

<style scoped>

</style>


