<script setup>
defineEmits(['again'])
</script>

<template>
    <div class="alert alert-success my-alert" role="alert">
        <div>Dziękujemy!</div>
        <div>Zgłoszenie zostało poprawnie wysłane.</div>
    </div>

    <div>
        Jeśli zarejestrowałeś wszystkie pojazdy możesz bezpiecznie zamknąć bieżącą zakładkę przeglądarki.
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