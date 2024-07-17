<script setup>
import { ref, reactive } from 'vue'
import { FontAwesomeIcon } from '@fortawesome/vue-fontawesome'
import { faRegistered } from '@fortawesome/free-solid-svg-icons'

import IntroView from './view/IntroView.vue'
import CongregationView from './view/CongregationView.vue'
import BusView from './view/BusView.vue'
import PilotIntroView from './view/PilotIntroView.vue'
import PilotDataView from './view/PilotDataView.vue'
import AdditionalInformation from './view/AdditionalInformation.vue'

import SummaryView from './view/SummaryView.vue'
import ConfirmationView from './view/ConfirmationView.vue'

const templateData = {
    congregation: "",
    bus: {
        type: "",
        distance: "",
        parking_mode: "not_needed"
    },
    one_pilot: true,
    pilot: [
        {
            firstname: "",
            lastname: "",
            email: "",
            phone: {
                direct: "+48",
                number: ""
            },
        },
        {
            firstname: "",
            lastname: "",
            email: "",
            phone: {
                direct: "+48",
                number: ""
            },
        },
        {
            firstname: "",
            lastname: "",
            email: "",
            phone: {
                direct: "+48",
                number: ""
            },
        }
    ],
    info: ""
}


const mode = ref(0)
let data = reactive(JSON.parse(JSON.stringify(templateData)))

function onAgain() {
    let newData = reactive(JSON.parse(JSON.stringify(templateData)))
    newData.congregation = data.congregation
    data = newData
    mode.value = 2
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
                v-model="data.congregation"
                @next="mode = 2" 
            />
            <BusView v-else-if="mode === 2"
                v-model="data.bus"
                @next="mode = 3"
                @back="mode = 1"
            />
            <PilotIntroView v-else-if="mode === 3"
                v-model="data.one_pilot"
                @next="mode = 4"
                @back="mode = 2"
            />
            <PilotDataView v-else-if="mode === 4"
                v-model="data.pilot[0]"
                :day="data.one_pilot ? '' : 'Piątek'"
                @next="mode = data.one_pilot ? 7 : 5"
                @back="mode = 3"
            />
            <PilotDataView v-else-if="mode === 5"
                v-model="data.pilot[1]"
                day="Sobota"
                @next="mode = 6"
                @back="mode = 4"
            />
            <PilotDataView v-else-if="mode === 6" 
                v-model="data.pilot[2]"
                day="Niedziela"
                @next="mode = 7"
                @back="mode = 5"
            />
            <AdditionalInformation v-else-if="mode === 7"
                v-model="data.info"
                @next="mode = 10"
                @back="mode = data.one_pilot ? 4 : 6"
            />

            <SummaryView v-else-if="mode === 10"
                :data="data"
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
