<script setup>
import { ref, computed } from 'vue'
import FooterButtons from '@/components/btns/FooterButtons.vue'
import TitleView from '@/components/TitleView.vue'
import SelectCongregation from '@/components/SelectCongregation.vue'
import ValidityInputGroup from '@/components/input/ValidityInputGroup.vue'

const props = defineProps(['modelValue'])

const congregationName = computed({
    get() {
        return props.modelValue
    },
    set(value) {
        emit('update:modelValue', value)
    }
})

const congregationNumber = ref()

const NextBtnEnabled = ref(true)

const emit = defineEmits(['update:modelValue', 'next'])
function onNextClicked() {
    emit('next')
}

function onSelectCongregationFinished(finished) {
    // NextBtnEnabled.value = 
    finished
}
</script>

<template>
    <div class="container">
        
        <TitleView>
            Logowanie do systemu
        </TitleView>

        <SelectCongregation 
            v-model="congregationName"
            @finished="onSelectCongregationFinished"
        />

        <ValidityInputGroup
            v-model="congregationNumber"
            class="mt-3"
            type="password"
            title="Hasło"
            required
        />

        <FooterButtons
            :back-visible="false"
            :next-enabled="NextBtnEnabled"
            @next="onNextClicked"
        />

    </div>
</template>