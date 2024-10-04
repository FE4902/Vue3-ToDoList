<script setup>
import Header from "./components/Header.vue";
import Todo from "./components/Todo.vue";
import Footer from "./components/Footer.vue";
import Modal from "./components/Modal.vue";
import { ref, watch } from "vue";

const filter = ref("ALL");
const todos = ref([
    { id: 1, text: "방 청소", isDone: true },
    { id: 2, text: "신발 정리", isDone: false },
    { id: 3, text: "코딩 공부", isDone: false },
]);

const filterTodos = ref([...todos.value]);

const insertTodo = (text) => {
    const insertTodoId =
        todos.value.length >= 1
            ? todos.value[todos.value.length - 1].id + 1
            : 1;

    todos.value = [...todos.value, { id: insertTodoId, text, isDone: false }];
};

watch(todos, () => {
    filterTodo(filter.value);
});

const handleFilter = (state) => {
    filter.value = state;
    filterTodo(filter.value);
};

const filterTodo = (value) => {
    switch (value) {
        case "ALL":
            filterTodos.value = [...todos.value];
            break;
        case "ACTIVE":
            filterTodos.value = [...todos.value].filter(
                (v) => v.isDone === false
            );
            break;
        case "COMPLETE":
            filterTodos.value = [...todos.value].filter(
                (v) => v.isDone === true
            );
            break;
    }
};

const clearTodo = (value) => {
    switch (value) {
        case "ALL":
            todos.value = [];
            filterTodos.value = [];
            break;
        case "COMPLETE":
            todos.value = [...todos.value].filter((v) => v.isDone === false);
            break;
    }
};
</script>

<template>
    <div class="wrap">
        <Header @insertTodo="insertTodo" />
        <Todo :todos="todos" :filterTodos="filterTodos" />
        <Footer
            :filter="filter"
            @handleFilter="handleFilter"
            @clearTodo="clearTodo"
        />
        <Modal />
    </div>
</template>

<style lang="scss" scoped>
.wrap {
    padding: 16px;
    margin: 16px;
    border: 1px solid black;
}
</style>
