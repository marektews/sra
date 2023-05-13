<script setup>
import FooterButtons from '@/components/btns/FooterButtons.vue'
import TitleView from '@/components/TitleView.vue'

const props = defineProps(['modelValue', 'day'])

const emit = defineEmits(['update:modelValue', 'back', 'next'])
function onNextClicked() {
    emit('next')
}
function onBackClicked() {
    emit('back')
}

</script>

<template>
    <div>
        <TitleView>
            Uwagi i dodatkowe informacje 
        </TitleView>

        <div>
            <textarea class="form-control" rows="6" 
                :value="props.modelValue" 
                @input="$emit('update:modelValue', $event.target.value)" 
            />

            <div class="alert alert-info mt-2">
                <h6>Uwaga!</h6>
                <div>Nie gwarantujemy preferowanych godzin odjazdu spod stadionu.</div>
                <div>Postaramy się uzględnić wszelkie uwagi, jeśli tylko będzie taka możliwość.</div>
            </div>
        </div>

        <FooterButtons
            @next="onNextClicked"
            @back="onBackClicked"
        />

    </div>
</template>