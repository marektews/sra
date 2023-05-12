<script setup>
import { ref } from 'vue'
import RegistrationForm from './view/RegistrationForm.vue'
import SummaryView from './view/SummaryView.vue'
import ConfirmationView from './view/ConfirmationView.vue'

const mode = ref(0)
</script>

<template>
    <header>
        <img src="@/assets/logo.svg" />
        <h2>System Rejestracji Autokarów</h2>
    </header>
    <main class="mt-4">
        <RegistrationForm v-if="mode === 0" @submit="mode = 1" />
        <SummaryView v-else-if="mode === 1" @submit="mode = 2"/>
        <ConfirmationView v-else @again="mode = 0" />
    </main>
</template>

<style scoped>
header {
    display: flex;
    align-items: center;
    gap: 16pt;
}
header > img {
    width: 50px;
    height: 50px;
}

main {
    min-width: 60vw;
    display: flex;
    flex-direction: column;
    flex-wrap: wrap;
    gap: 9pt;
}

main > div {
    flex-grow: 1;
}
</style>
