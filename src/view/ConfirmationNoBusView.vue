<script setup>
import { FontAwesomeIcon } from '@fortawesome/vue-fontawesome';
import { faPhone, faEnvelope } from '@fortawesome/free-solid-svg-icons';
</script>

<template>
    <div class="alert alert-success my-alert" role="alert">
        <div>Dziękujemy!</div>
        <div>Informacja została poprawnie wysłana.</div>
    </div>

    <div class="alert alert-secondary my-info" role="alert">
        <h5>Kontakt z działem parkingów:</h5>
        <div style="font-weight: bold;">Jakub Krzyszczak</div>
        <div><FontAwesomeIcon :icon="faPhone" /> +48533515555</div>
        <div><FontAwesomeIcon :icon="faEnvelope"/> JKrzyszczak1@jwpub.org</div>
    </div>

    <div class="alert alert-warning my-info" role="alert">
        Możesz już bezpiecznie zamknąć bieżącą zakładkę przeglądarki.
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