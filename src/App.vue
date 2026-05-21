<script setup>
import { ref, reactive } from 'vue'
import { FontAwesomeIcon } from '@fortawesome/vue-fontawesome'
import { faRegistered } from '@fortawesome/free-solid-svg-icons'

import IntroView from '@/view/IntroView.vue'
import CongregationView from '@/view/CongregationView.vue'
import BusView from '@/view/BusView.vue'
import PilotIntroView from '@/view/PilotIntroView.vue'
import PilotDataView from '@/view/PilotDataView.vue'
import AdditionalInformation from '@/view/AdditionalInformation.vue'

import SummaryView from '@/view/SummaryView.vue'
import ConfirmationView from '@/view/ConfirmationView.vue'

const mode = ref(0)
const congregation = ref('')
const info = ref('')
const one_pilot = ref(true)
let bus = reactive({
    type: "",
    distance: "",
    parking_mode: "not_needed"
})
let pilot_1 = reactive({
    firstname: "",
    lastname: "",
    email: "",
    phone: {
        direct: "+48",
        number: ""
    },
})
let pilot_2 = reactive({
    firstname: "",
    lastname: "",
    email: "",
    phone: {
        direct: "+48",
        number: ""
    },
})
let pilot_3 = reactive({
    firstname: "",
    lastname: "",
    email: "",
    phone: {
        direct: "+48",
        number: ""
    },
})

function onAgain() {
    mode.value = 2
    one_pilot.value = true
    info.value = ''
    bus = reactive({
        type: "",
        distance: "",
        parking_mode: "not_needed"
    })
    pilot_1 = reactive({   
        firstname: "",
        lastname: "",
        email: "",
        phone: {
            direct: "+48",
            number: ""
        },
    })
    pilot_2 = reactive({
        firstname: "",
        lastname: "",
        email: "",
        phone: {
            direct: "+48",
            number: ""
        },
    })
    pilot_3 = reactive({
        firstname: "",
        lastname: "",
        email: "",
        phone: {
            direct: "+48",
            number: ""
        },
    })
}
</script>

<template>
    <div class="container">
        <header>
            <!-- <img src="@/assets/logo.svg" /> -->
            <FontAwesomeIcon :icon="faRegistered" size="3x" />
            <div>Ankieta rejestracji autokarów / autobusów</div>
        </header>

        <main class="mt-4">
            <IntroView v-if="mode === 0" @next="mode = 1" />
            <CongregationView v-else-if="mode === 1"
                v-model="congregation"
                @next="mode = 2" 
            />
            <BusView v-else-if="mode === 2"
                v-model="bus"
                @next="mode = 3"
                @back="mode = 1"
            />
            <PilotIntroView v-else-if="mode === 3"
                v-model="one_pilot"
                @next="mode = 4"
                @back="mode = 2"
            />
            <PilotDataView v-else-if="mode === 4"
                v-model="pilot_1"
                :day="one_pilot ? '' : 'Piątek'"
                @next="mode = one_pilot ? 7 : 5"
                @back="mode = 3"
            />
            <PilotDataView v-else-if="mode === 5"
                v-model="pilot_2"
                day="Sobota"
                @next="mode = 6"
                @back="mode = 4"
            />
            <PilotDataView v-else-if="mode === 6" 
                v-model="pilot_3"
                day="Niedziela"
                @next="mode = 7"
                @back="mode = 5"
            />
            <AdditionalInformation v-else-if="mode === 7"
                v-model="info"
                @next="mode = 10"
                @back="mode = one_pilot ? 4 : 6"
            />

            <SummaryView v-else-if="mode === 10"
                :congregation="congregation"
                :bus="bus"
                :one_pilot="one_pilot"
                :pilot="[pilot_1, pilot_2, pilot_3]"
                :info="info"
                @correction="mode = $event"
                @back="mode = 7"
                @submit="mode = 11"
            />

            <ConfirmationView v-else 
                @again="onAgain" 
            />
        </main>
    </div>
</template>

<style scoped>
header {
    display: flex;
    align-items: center;
    gap: 16pt;
    margin-bottom: 24pt;
}
header > div {
    font-size: 2rem;
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
