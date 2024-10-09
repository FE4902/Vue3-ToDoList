<script setup>
import { onMounted } from "vue";

onMounted(() => {
    document.querySelector(".modal").show();
});
</script>

<template>
    <dialog class="modal">
        <div class="modal__body">
            <h4>Edit Todo</h4>
            <div>선택한 텍스트</div>
            <div>
                <input type="text" />
            </div>
            <div class="">
                <button>Confirm</button>
                <button>Cancel</button>
            </div>
        </div>
    </dialog>
</template>

<style lang="scss" scoped>
.modal {
}
</style>
