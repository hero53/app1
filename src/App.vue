
<style scoped></style>
<template>
  <div id="top">
    <span id="up"></span>
    <h1>#App_1</h1>
    <TodoHeader>
      <template v-slot:completed>
        {{ todoDone }}
      </template>
      <template v-slot:countName>
        {{ todoList.length }}
      </template>
    </TodoHeader>

    <main>
     
      <TodoInput  @addTodo="addTodo" @removeTodo="removeTodo"/>

      <div id="todoList" v-for="todo in todoList" :key="todo.id">
        <!-- <div class="listItem">
          <div :class="{ 'todoNameDone': todo.is_done, 'todoName': !todo.is_done }" @click="handleToggler(todo.id)">{{
            todo.task }}</div>
          <button type="button" @click="handleDelete(todo.id)">×</button>
        </div> -->
        <TodoItem :todo="todo" @handleToggler="handleToggler" @handleDelete="handleDelete"/>
      </div>
    </main>
  </div>
</template>



<script setup>

//IMPORTATION 
import { computed, ref } from "vue";
import TodoHeader from './components/TodoHeader.vue';
import TodoInput from './components/TodoInput.vue';
import TodoItem from './components/TodoItem.vue';
import TODOLIST from "./model/todolist";

//states
let todoList = ref(TODOLIST);

// action
const handleToggler = (id) => {
  let copyTask = [...todoList.value];
  let taskIndex = copyTask.findIndex(todo => todo.id === id);
  copyTask[taskIndex].is_done = !copyTask[taskIndex].is_done;
  todoList.value = copyTask;
};


const addTodo = (data) => {
  let copyTask = [...todoList.value];
  let newId = parseInt(todoList.value.length) + 1
  copyTask.push({ "id": newId, "task": data, "is_done": false });
  todoList.value = copyTask;
}


const handleDelete = (id) => {
  let newTodoList = todoList.value.filter(todo => todo.id !== id);
  todoList.value = newTodoList;
}


const todoDone = computed(() => {
  return todoList.value.filter(todo => todo.is_done).length;
});

</script>
