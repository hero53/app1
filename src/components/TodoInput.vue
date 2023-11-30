
<style scoped></style>
<template>
    <div id="todoInput">
        <div class="listItem">
            <input type="text" v-model="newTodo" placeholder="Ajouter une tâche" @keydown.enter="add"
                @keydown.esc="removeTodo">
        </div>
    </div>
</template>



<script setup>

import { defineProps, ref,getCurrentInstance } from "vue";
const { emit } = getCurrentInstance();
const newTodo = ref('')

const { addTodo } = defineProps([ 'addTodo']);
const add = (e) => {
    e.preventDefault()
    emit("addTodo", newTodo.value);
    newTodo.value = ""
}

const removeTodo = (e) => {
  e.preventDefault()
  newTodo.value = ""
}


</script>
