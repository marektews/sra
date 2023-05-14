<script setup>
import TitleView from '@/components/TitleView.vue'

const emit = defineEmits('next')
function onNextClicked() {
    emit('next')
}
</script>

<template>
    <div class="container">
        
        <TitleView>
            Witaj w systemie rejestracji autokarów
        </TitleView>

        <div>
            Zaloguj się za pomocą otrzymanych danych i uważnie wypełnij formularz.
        </div>

        <button class="mt-5 btn btn-lg btn-outline-primary" @click="onNextClicked">
            ZACZYNAMY
        </button>

    </div>
</template>