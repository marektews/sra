<script setup>
import FooterButtons from '@/components/btns/FooterButtons.vue'
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
            <div>... jakieś zgrabne info ...</div>
        </div>

        <FooterButtons 
            @click="onNextClicked"
            :back-visible="false"
        />

    </div>
</template>