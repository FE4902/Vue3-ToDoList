<script setup>
import Header from "./components/Header.vue";
import Todo from "./components/Todo.vue";
import Footer from "./components/Footer.vue";
import Modal from "./components/Modal.vue";
import { ref, watch } from "vue";

const todos = ref([
    { id: 1, text: "방 청소", isDone: true },
    { id: 2, text: "신발 정리", isDone: false },
    { id: 3, text: "코딩 공부", isDone: false },
]);
const editModal = ref(false);
const editTodo = ref({ id: 0, text: "", isDone: false });

const filter = ref("ALL");
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

const handleEditModal = (id) => {
    editModal.value = true;
    editTodo.value = todos.value.find((v) => v.id === id);

    document.querySelector(".modal").showModal();
};

const handleEditTodo = (object) => {
    todos.value = [
        ...todos.value.filter((v) => v.id !== editTodo.id),
        ...editTodo,
    ].sort((a, b) => a - b);
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
        <Todo
            :todos="todos"
            :filterTodos="filterTodos"
            @handleEditModal="handleEditModal"
        />
        <Footer
            :filter="filter"
            @handleFilter="handleFilter"
            @clearTodo="clearTodo"
        />
        <Modal :editTodo="editTodo" @handleEditTodo="handleEditTodo" />
    </div>
</template>

<style lang="scss" scoped>
.wrap {
    padding: 16px;
    border: 1px solid black;
}
</style>
