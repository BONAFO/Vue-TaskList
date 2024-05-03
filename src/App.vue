<script setup>
import { ref } from "vue";

const tasks = ref([]);
let counter = 0;
const inputtask = ref("");

const add_task = () => {
  tasks.value.push({ task: inputtask.value, completed: false, id: counter , update: false , aux : inputtask.value });
  counter++;
  inputtask.value = "";
};

const delete_task = (index) => {
  tasks.value = tasks.value.filter((t) => t.id !== index);
};

const update_task = (id) => {
  const index = tasks.value.indexOf( tasks.value.filter((t) => t.id === id )[0]);
  if(index != -1){
    tasks.value[index].task = tasks.value[index].aux
    tasks.value[index].update = false
  }
};

</script>

<template>
  <div class="container f-c">
    <input v-model="inputtask" type="text" />
  <button class="btn-send" @click="add_task">CREATE TASK</button>
  </div>

  <br />

  <ol>
    <div :key="task.id" v-for="task in tasks">

      <li>
        <div v-if="!task.update">
          <h3>{{ task.task }}</h3>
          <button class="btn btn-mod" @click="()=>{task.update = true}">MOD</button>
          <button class="btn btn-del" @click="delete_task(task.id)">X</button>
        </div>

        <div v-else>
          <input type="text" class="input-mod" v-model="task.aux">
          <button class="btn btn-save" @click="update_task(task.id)">SAVE</button>
          <button class="btn btn-del" @click="()=>{task.update = false}">X</button>
        </div>
      </li>
    </div>
  </ol>
</template>

<style scoped>
@import './style/style.css';
</style>
