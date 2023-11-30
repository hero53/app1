
<style scoped></style>
<template>
    <div class="listItem">
        <div :class="{ 'todoNameDone': todo.is_done, 'todoName': !todo.is_done }" @click="toggler(todo.id)">{{
            todo.task }}</div>
        <button type="button" @click="remove(todo.id)">×</button>
    </div>
</template>



<script setup>

import { defineProps, getCurrentInstance } from "vue";
const { emit } = getCurrentInstance();

const { todo,handleToggler,handleDelete } = defineProps(['todo','handleToggler','handleDelete']);

const toggler = (id)=>{
    emit("handleToggler", id);
}

const remove = (id) => {
    emit("handleDelete", id);
}

</script>
