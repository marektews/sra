<script setup>
// import TitleView from '@/components/TitleView.vue'

const emit = defineEmits('next')
function onNextClicked() {
    emit('next')
}
</script>

<template>
    <div class="container">
        
        <!-- <TitleView>
            Witamy!
        </TitleView> -->

        <h5>
            Zaloguj się za pomocą otrzymanych danych i uważnie wypełnij formularz.
        </h5>

        <button class="mt-5 btn btn-lg btn-outline-primary" @click="onNextClicked">
            ZACZYNAMY
        </button>

    </div>
</template>