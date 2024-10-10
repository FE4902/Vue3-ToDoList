<script setup>
const props = defineProps({
    todos: Array,
    filterTodos: Array,
});
const emit = defineEmits(["handleEditModal"]);
</script>

<template>
    <ul class="todo">
        <li class="todo__item" v-for="todo in props.filterTodos" :key="todo.id">
            <input
                class="todo__checkbox"
                type="checkbox"
                v-model="todo.isDone"
            />
            <span class="todo__text" :class="{ complete: todo.isDone }">{{
                todo.text
            }}</span>
            <button @click="emit('handleEditModal', todo.id)">✏️</button>
        </li>
    </ul>
</template>

<style lang="scss" scoped>
.todo {
    &__item {
        display: flex;
        align-content: center;
        gap: 8px;
    }

    &__text {
        &.complete {
            text-decoration: line-through;
        }
    }

    &__checkbox {
        accent-color: black;
    }
}
</style>
