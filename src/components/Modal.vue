<script setup>
import { ref, onMounted } from "vue";

const props = defineProps({ editTodo: Object });
const emit = defineEmits(["handleEditTodo"]);

const closeModal = () => {
    document.querySelector(".modal").close();
};
</script>

<template>
    <dialog class="modal">
        <h4>Edit Todo</h4>
        <div>{{ editTodo.text }}</div>
        <div>
            <input type="text" :value="editTodo.text" />
        </div>
        <div class="modal__buttons">
            <button class="modal__button" @click="handleEditTodo">
                Confirm
            </button>
            <button class="modal__button" @click="closeModal">Cancel</button>
        </div>
    </dialog>
</template>

<style lang="scss" scoped>
.modal {
    margin: auto;

    &::backdrop {
        background-color: rgba(black, 0.5);
        backdrop-filter: blur(1px);
    }

    &__buttons {
        display: flex;
        justify-content: center;
        align-items: center;
        gap: 4px;
    }

    &__button {
        padding: 2px 4px;
        border: 1px solid black;

        &:hover {
            color: white;
            background-color: black;
        }
    }
}
</style>
