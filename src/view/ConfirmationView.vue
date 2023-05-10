<script setup>
const emit = defineEmits(['again'])

const onAgain = () => {
    emit('again')
}
</script>

<template>
    <div class="alert alert-success" role="alert">
        Zgłoszenie zostało poprawnie wysłane. Dziękujemy!
    </div>

    <div>
        <button class="btn btn-lg btn-outline-primary" @click="onAgain">
            Zarejestruj następny pojazd
        </button>
    </div>
</template>

<style>
.alert {
    font-size: 1.3rem;
}
</style>