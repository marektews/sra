<script setup>
const emit = defineEmits('submit')

function onSubmit() {
    emit('submit')
}
</script>

<template>
    <div>
        <div>TODO: Podsumowanie</div>

        <button class="btn btn-lg btn-outline-primary" @click="onSubmit">
            Wyślij zgłoszenie
        </button>
    </div>
</template>