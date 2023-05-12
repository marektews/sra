<script setup>
const emit = defineEmits(['again'])

const onAgain = () => {
    emit('again')
}
</script>

<template>
    <div class="alert alert-success my-alert" role="alert">
        Zgłoszenie zostało poprawnie wysłane. Dziękujemy!
    </div>

    <div>
        <button class="btn btn-lg btn-outline-primary" @click="onAgain">
            Zarejestruj następny pojazd
        </button>
    </div>
</template>

<style scoped>
.my-alert {
    font-size: 1.3rem;
}
</style>