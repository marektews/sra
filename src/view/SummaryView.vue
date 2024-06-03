<script setup>
import { ref, computed } from 'vue'
import FooterButtons from '@/components/btns/FooterButtons.vue'
import TitleView from '@/components/TitleView.vue'
import ValidityInputGroup from '../components/input/ValidityInputGroup.vue';

const props = defineProps(['data'])
const emit = defineEmits('submit', 'back', 'correction')

const confirmationEmail = ref('')

function strBusType(v) {
    switch(v) {
        case "minibus_9": return "minibus do 9 osób"
        case "minibus_30": return "minibus do 30 osób"
        case "autokar_50": return "autokar do 50 osób"
        case "autokar_70": return "autokar 60-70 osób"
        case "autobus_12m": return "autobus miejski - 12m (pojedyńczy)"
        case "autobus_18m": return "autobus miejski - 18m (przegubowy)"
    }
    return v
}

function strBusDistance(v) {
    switch(v) {
        case "15km": return "do 15 km"
        case "25km": return "do 25 km"
        case "50km": return "do 50 km"
        case "100km": return "do 100 km"
        case "200km": return "do 200 km"
        case "more200km": return "powyżej 200 km"
    }
    return v
}

function strBusParking(v) {
    switch(v) {
        case "needed": return "potrzebne miejsce parkingowe"
        case "not_needed": return "pojazd tylko dowozi pasażerów, odjeżdza i przyjeżdza odebrać ich po programie"
    }
    return v
}

function strPilotMode(v) {
    if(v)
        return "Jeden pilot we wszystkie dni kongresowe"
    else
        return "Kilku pilotów zajmuje się obsługą pojazdu"
}

function strDayName(idx) {
    switch(idx) {
        case 0: return "Piątek"
        case 1: return "Sobota"
        case 2: return "Niedziela"
    }
    return idx
}

const isSubmitEnabled = ref(false)

function onSubmit() {
    let bodyData = {
        registration_data: props.data,
        confirmation_email: confirmationEmail.value
    }
    fetch('/api/sra/submit', {
        method: "POST",
        cache: "no-cache",
        headers: {
            "Content-Type": "application/json",
        },
        body: JSON.stringify(bodyData)
    })
    .then(resp => {
        if(resp.status === 200) {
            emit('submit')
        }
    })
    .catch(e => console.error("Submit SRA", e))
}
</script>

<template>
    <div class="container">
        <TitleView>
            Podsumowanie
        </TitleView>

        <div class="alert alert-danger d-flex flex-row align-items-baseline">
            <div>
                <i class="fa-solid fa-circle-exclamation"></i>
            </div>
            <div class="ms-2">
                <div>
                    Bardzo prosimy o uważne sprawdzenie poprawności wprowadzonych danych przed wysłaniem zgłoszenia.
                </div>
                <div>
                    Jeśli jest coś do poprawki kliknij w błędną wartość, a zostaniesz przekierowany w odpowiednie miejsce.
                </div>
            </div>
        </div>

        <div class="summary-layout">
            <div class="summary-cell-title">Dane pojazdu</div>
            
            <div class="summary-cell-label">Zbór:</div>
            <div class="summary-cell-value">
                <a href="#" @click="$emit('correction', 1)">
                    {{props.data.congregation}}
                </a>
            </div>

            <div class="summary-cell-label">Długość trasy:</div>
            <div class="summary-cell-value">
                <a href="#" @click="$emit('correction', 2)">
                    {{ strBusDistance(props.data.bus.distance) }}
                </a>
            </div>

            <div class="summary-cell-label">Typ pojazdu:</div>
            <div class="summary-cell-value">
                <a href="#" @click="$emit('correction', 2)">
                    {{ strBusType(props.data.bus.type) }}
                </a>
            </div>

            <div class="summary-cell-label">Parking:</div>
            <div class="summary-cell-value">
                <a href="#" @click="$emit('correction', 2)">
                    {{ strBusParking(props.data.bus.parking_mode) }}
                </a>
            </div>


            <div class="summary-cell-title">Dane kontaktowe pilota</div>

            <template v-if="props.data.one_pilot">
                <div class="summary-cell-label">Imię i nazwisko:</div>
                <div class="summary-cell-value">
                    <a href="#" @click="$emit('correction', 4)">
                        {{ props.data.pilot[0].firstname }} {{ props.data.pilot[0].lastname }}
                    </a>
                </div>
                
                <div class="summary-cell-label">Numer telefonu:</div>
                <div class="summary-cell-value">
                    <a href="#" @click="$emit('correction', 4)">
                        {{ props.data.pilot[0].phone.direct }} {{ props.data.pilot[0].phone.number }}
                    </a>
                </div>

                <div class="summary-cell-label">Adres e-mail:</div>
                <div class="summary-cell-value">
                    <a href="#" @click="$emit('correction', 4)">
                        {{ props.data.pilot[0].email }}
                    </a>
                </div>

                <div class="mt-5"/>
                <div class="summary-cell-value">
                    <a href="#" @click="$emit('correction', 3)">
                        <i class="fa-solid fa-circle-exclamation" />
                        {{ strPilotMode(props.data.one_pilot) }}
                    </a>
                </div>
            </template>
            <template v-else>
                <template v-for="(pilot, index) in props.data.pilot" :key="index">
                    <div class="summary-cell-value" :class="{'mt-4': index}">{{ strDayName(index) }}</div>
                    <div/>
                    
                    <div class="summary-cell-label">Imię i nazwisko:</div>
                    <div class="summary-cell-value">
                        <a href="#" @click="$emit('correction', 4+index)">
                            {{ pilot.firstname }} {{ pilot.lastname }}
                        </a>
                    </div>
                    
                    <div class="summary-cell-label">Numer telefonu:</div>
                    <div class="summary-cell-value">
                        <a href="#" @click="$emit('correction', 4+index)">
                            {{ pilot.phone.direct }} {{ pilot.phone.number }}
                        </a>
                    </div>

                    <div class="summary-cell-label">Adres e-mail:</div>
                    <div class="summary-cell-value">
                        <a href="#" @click="$emit('correction', 4+index)">
                            {{ pilot.email }}
                        </a>
                    </div>
                </template>
                
                <div class="mt-5"/>
                <div class="summary-cell-value">
                    <a href="#" @click="$emit('correction', 3)">
                        <i class="fa-solid fa-circle-exclamation" />
                        {{ strPilotMode(props.data.one_pilot) }}
                    </a>
                </div>
            </template>

            <div class="summary-cell-title">Uwagi i dodatkowe informacje</div>
            <div class="summary-cell-label">Treść:</div>
            <div class="summary-cell-value multiline">
                <a href="#" @click="$emit('correction', 7)">
                    <span v-if="props.data.info.length">
                        {{ props.data.info }}
                    </span>
                    <span v-else>
                        # Nie podano żadnych informacji #
                    </span>
                </a>
            </div>
        </div>

        <div class="alert alert-success">
            <ValidityInputGroup
                v-model="confirmationEmail"
                type="email"
                title="Adres e-mail do potwierdzenia rejestracji (inny niż w domienie @jwpub.org)"
                placeholder="nazwa@domena.pl"
                required
                @valid="isSubmitEnabled = true"
            />
            <div class="mt-3">
                <div>Podaj swój prywatny adres poczty elektronicznej, aby otrzymać potwierdzenie wysłania zgłoszenia.</div>
                <div>Nic nie będziesz musiał odsyłać. Otrzymasz tylko do wglądu kopię tego zgłoszenia.</div>
            </div>
        </div>

        <FooterButtons
            :next-visible="false"
            :submit-visible="true"
            :submit-enabled="isSubmitEnabled"
            @back="$emit('back')"
            @submit="onSubmit"
        />
    </div>
</template>

<style scoped>
.summary-layout {
    margin-top: 2rem;
    margin-bottom: 4rem;
    display: grid;
    grid-template-columns: auto 1fr;
    align-items: first baseline;
    gap: 0 16pt;
}

.row-span, 
.summary-cell-title {
    grid-column: 1 / 3;
}

.summary-cell-title {
    font-size: 1.5rem;
    margin-bottom: 0.8rem;
}
.summary-cell-title:not(:first-child) {
    padding-top: 2rem;
}

.summary-cell-label {
    font-size: 0.9rem;
}

.summary-cell-value {
    font-size: 1.2rem;
    color: var(--color-heading);
}

.multiline {
    white-space: pre-wrap;
}
</style>