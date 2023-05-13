<script setup>
import { ref, computed } from 'vue'
import FooterButtons from '@/components/btns/FooterButtons.vue'
import TitleView from '@/components/TitleView.vue'
import SelectCongregation from '@/components/SelectCongregation.vue'

const props = defineProps(['modelValue'])

const congregation = computed({
    get() {
        return props.modelValue
    },
    set(value) {
        emit('update:modelValue', value)
    }
})

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
            Nazwa zboru
        </TitleView>

        <SelectCongregation 
            v-model="congregation"
            @finished="onSelectCongregationFinished"
        />

        <FooterButtons
            :back-visible="false"
            :next-enabled="NextBtnEnabled"
            @next="onNextClicked"
        />

    </div>
</template>