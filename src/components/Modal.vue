<script setup>
import { ref, onMounted } from "vue";

const props = defineProps({ editTodo: Object });
const emit = defineEmits(["handleEditTodo"]);

onMounted(() => {
    document.querySelector(".modal").show();
});
</script>

<template>
    <dialog class="modal">
        <div class="modal__body">
            <h4>Edit Todo</h4>
            <div>{{ editTodo.text }}</div>
            <div>
                <input type="text" :value="editTodo.text" />
            </div>
            <div class="">
                <button @click="handleEditTodo">Confirm</button>
                <button>Cancel</button>
            </div>
        </div>
    </dialog>
</template>

<style lang="scss" scoped>
.modal {
}
</style>
