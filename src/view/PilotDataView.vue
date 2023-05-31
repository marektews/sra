<script setup>
import { ref, reactive, computed, onBeforeUnmount } from 'vue'
import FooterButtons from '@/components/btns/FooterButtons.vue'
import TitleView from '@/components/TitleView.vue'
import ValidityInput from '@/components/input/ValidityInput.vue'
import ValidityInputGroup from '@/components/input/ValidityInputGroup.vue'

const props = defineProps(['modelValue', 'day'])
const emit = defineEmits(['update:modelValue', 'back', 'next'])

const pilot = reactive(props.modelValue)
const dupPilot = ref(false)
const timer = ref(null)

const onPhoneDirectChanged = (e) => {
    e.target.reportValidity()
}
const phoneLength = computed(() => {
    return pilot.phone.direct === "+7" ? 10 : 9
})
const phoneFormat = computed(() => {
    if(phoneLength.value === 10)
        return "Wpisz 10 cyfr; format: 1234567890"
    else
        return "Wpisz 9 cyfr; format: 123456789"
})
const phonePattern = computed(() => {
    return pilot.phone.direct === "+7"
        ? "[0-9]{10}"
        : "[0-9]{9}"
})

onBeforeUnmount(() => {
    if(timer.value != null) {
        clearTimeout(timer.value)
        timer.value = null
    }
})

function onNextClicked() {
    emit('update:modelValue', pilot)

    let data = {
        phone: pilot.phone
    }
    fetch('/api/sra/check_pilot_duplicate', {
        method: "POST",
        headers: {
            "Content-Type": "application/json",
        },
        body: JSON.stringify(data)
    })
    .then(response => {
        if(response.status === 200) {
            emit('next')
        }
        else {
            dupPilot.value = true
            if(timer.value == null) {
                timer.value = setTimeout(() => { 
                    dupPilot.value = false
                    clearTimeout(timer.value)
                    timer.value = null
                }, 10000)
            }
        }
    })
}
function onBackClicked() {
    emit('update:modelValue', pilot)
    emit('back')
}

const validValues = ref([false, false, false, false])

const isNextBtnEnabled = computed(() => {
    return !validValues.value.includes(false)
})
</script>

<template>
    <div class="container">
        <TitleView>
            Dane kontaktowe zborowego pilota dedykowanego do autokaru / autobusu / busa
        </TitleView>

        <div v-if="day.length > 0" class="mt-3">
            Dzień: <span class="day ms-1">{{ day }}</span>
        </div>

        <ValidityInputGroup
            class="mt-3"
            v-model="pilot.firstname"
            title="Imię"
            required
            @valid="validValues[0] = $event"
        />

        <ValidityInputGroup
            class="mt-3"
            v-model="pilot.lastname"
            title="Nazwisko"
            required
            @valid="validValues[1] = $event"
        />

        <div class="mt-3">
            <label class="form-label">Numer telefonu</label>
            <div class="input-group">
                <select 
                    v-model="pilot.phone.direct"
                    class="form-select form-select-lg flex-grow-0" 
                    style="min-width: 90pt"
                    @change="onPhoneDirectChanged"
                >
                    <option value="+48">PL: +48</option>
                    <option value="+7">RU: +7</option>
                    <option value="+380">UA: +380</option>
                </select>
                <ValidityInput
                    v-model="pilot.phone.number"
                    type="tel"
                    :maxlength="phoneLength"
                    :pattern="phonePattern"
                    :placeholder="phoneFormat"
                    required
                    @valid="validValues[2] = $event"
                />
            </div>
        </div>

        <ValidityInputGroup
            class="mt-3"
            v-model="pilot.email"
            title="Podaj prywatny adres poczty elektronicznej (inny niż w domienie @jwpub.org)"
            type="email"
            placeholder="nazwa_konta@domena.pl"
            required
            @valid="validValues[3] = $event"
        />

        <div v-if="dupPilot" class="alert alert-danger mt-4">
            <div>UWAGA!</div>
            <div>Ten sam pilot nie może być przypisany do dwóch pojazdów - podaj dane innego pilota.</div>
        </div>

        <FooterButtons
            @next="onNextClicked"
            @back="onBackClicked"
            :next-enabled="isNextBtnEnabled"
        />

    </div>
</template>

<style scoped>
.day {
    font-size: 1.4rem;
    font-weight: bold;
}
</style>