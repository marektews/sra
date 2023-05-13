<script setup>
defineEmits(['again'])
</script>

<template>
    <div class="alert alert-success my-alert" role="alert">
        Zgłoszenie zostało poprawnie wysłane. Dziękujemy!
    </div>

    <div class="mt-5">
        <button class="btn btn-lg btn-outline-primary" @click="$emit('again')">
            Zarejestruj następny pojazd
        </button>
    </div>
</template>

<style scoped>
.my-alert {
    font-size: 1.3rem;
}
</style>