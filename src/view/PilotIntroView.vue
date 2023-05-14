<script setup>
import { computed } from 'vue'
import FooterButtons from '@/components/btns/FooterButtons.vue'
import TitleView from '@/components/TitleView.vue'

const props = defineProps(['modelValue'])

const one_pilot = computed({
    get() {
        return props.modelValue
    },
    set(value) {
        emit('update:modelValue', value)
    }
})

const emit = defineEmits(['update:modelValue', 'back', 'next'])
function onNextClicked() {
    emit('next')
}
function onBackClicked() {
    emit('back')
}
</script>

<template>
    <div class="container">
        <TitleView>
            Konfiguracja pilotów dedykowanych do autokaru / autobusu / busa
        </TitleView>

        <div class="form-check my-5">
            <input class="form-check-input" type="checkbox" id="sp" v-model="one_pilot" />
            <label class="form-check-label" for="sp">
                <div>Jeden pilot we wszystkie dni kongresowe</div>
                <small>Po odznaczeniu tej opcji system rejestracji poprosi o podanie danych pilotów na każdy dzień kongresowy</small>
            </label>
        </div>

        <FooterButtons
            @next="onNextClicked"
            @back="onBackClicked"
        />

    </div>
</template>