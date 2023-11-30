
<style scoped></style>
<template>
    <header>
        <h1>Todo</h1>
        <div id="todoStatus">
            <div id="totalComp">
                <span id="totalCompleted" class="countData">
                    <slot name="completed"></slot>
                </span><span class="countName">Complet</span>
            </div>
            <div id="totalNum">
                <span id="totalTodos" class="countData">
                    <slot name="countName"></slot>

                </span><span class="countName">Total</span>
            </div>
        </div>
    </header>
</template>



<script setup>
</script>
