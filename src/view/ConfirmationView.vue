<script setup>
defineEmits(['again'])
</script>

<template>
    <div class="alert alert-success my-alert" role="alert">
        <div>Dziękujemy!</div>
        <div>Zgłoszenie zostało poprawnie wysłane.</div>
    </div>

    <div class="alert alert-warning my-info" role="alert">
        <div>
            Dodatkowe informacje:
        </div>
        <ol>
            <li class="mt-2">
                <div>
                    Pilot lub osoba rejestrująca będą mogli pobrać identyfikator autokaru
                    w późniejszym terminie.
                </div>
                <div>
                    Informacja o możliwości pobrania identyfikatora wraz z godziną odjazdu
                    będzie wysłana drogą mailową.
                </div>
            </li>
            <li class="mt-2">
                Jeśli zarejestrowałeś wszystkie pojazdy możesz bezpiecznie zamknąć bieżącą zakładkę przeglądarki.
            </li>
        </ol>
    </div>

    

    <div class="mt-5">
        <button class="btn btn-lg btn-outline-primary me-2" @click="$emit('again')">
            Zarejestruj następny pojazd
        </button>
    </div>
</template>

<style scoped>
.my-alert {
    font-size: 1.3rem;
}
.my-info {
    font-size: 1.1rem;
}
</style>