
<style scoped></style>

<template>
  <div id="top">
    <span id="up"></span>
    <h1>#App_1</h1>
    <header>
      <h1>Todo</h1>
      <div id="todoStatus">
        <div id="totalComp">
          <span id="totalCompleted" class="countData">{{ todoDone }}</span><span class="countName">Complet</span>
        </div>
        <div id="totalNum">
          <span id="totalTodos" class="countData">{{ todoList.length }}</span><span class="countName">Total</span>
        </div>
      </div>
    </header>
    <main>
      <div id="todoInput">
        <div class="listItem">
          <input type="text" v-model="newTodo" placeholder="Input here and return to add..." @keydown.enter="addTodo"
            @keydown.esc="removeTodo">
        </div>
      </div>
      <div id="todoList" v-for="todo in todoList" :key="todo.id">
        <div class="listItem">
          <div :class="{ 'todoNameDone': todo.is_done, 'todoName': !todo.is_done }" @click="handleToggler(todo.id)">{{
            todo.task }}</div>
          <button type="button" @click="handleDelete(todo.id)">×</button>
        </div>
      </div>
    </main>
  </div>
</template>



<script setup>
import { computed, ref } from "vue";
//state
let todoList = ref([
  {
    "id": 1,
    "task": "Faire les courses",
    "is_done": false
  },
  {
    "id": 2,
    "task": "Répondre aux emails",
    "is_done": true
  },
  {
    "id": 3,
    "task": "Faire du sport",
    "is_done": false
  },
  {
    "id": 4,
    "task": "Lire un livre",
    "is_done": true
  },
  {
    "id": 5,
    "task": "Travailler sur un projet",
    "is_done": false
  }
]
);
const newTodo = ref('')
// action 


const handleToggler = (id) => {
  let copyTask = [...todoList.value];
  let taskIndex = copyTask.findIndex(todo => todo.id === id);
  copyTask[taskIndex].is_done = !copyTask[taskIndex].is_done;
  todoList.value = copyTask;
};

const addTodo = (e) => {
  e.preventDefault()
  let copyTask = [...todoList.value];
  let newId = parseInt(todoList.value.length) + 1
  copyTask.push({ "id": newId, "task": newTodo.value, "is_done": false });
  todoList.value = copyTask;
  newTodo.value = ""
  console.log(copyTask);
}
const handleDelete = (id) => {
  let newTodoList = todoList.value.filter(todo => todo.id !== id);
  todoList.value = newTodoList;
}


const todoDone = computed(() => {
  return todoList.value.filter(todo => todo.is_done).length;
});
</script>
