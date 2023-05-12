<script setup>
import { ref, reactive } from 'vue'
import SelectCongregation from '../components/SelectCongregation.vue'

const emit =  defineEmits('submit')
const onSubmit = () => {
    emit('submit')
}

const single_pilot = ref(true)

const pilot1 = reactive({
    firstname: "",
    lastname: "",
    phone: {
        direct: "+48",
        number: ""
    },
    email: {
        login: "",
        domain: ""
    }
})

const pilot2 = reactive({
    firstname: "",
    lastname: "",
    phone: {
        direct: "+48",
        number: ""
    },
    email: {
        login: "",
        domain: ""
    }
})

const pilot3 = reactive({
    firstname: "",
    lastname: "",
    phone: {
        direct: "+48",
        number: ""
    },
    email: {
        login: "",
        domain: ""
    }
})


</script>

<template>
    <div>
        <div class="alert alert-info alert-layout" role="alert">
            <i class="fa-solid fa-circle-info"></i>
            <div>
                Jeżeli macie wynajętych więcej niż jeden autokar/autobus, 
                to w poniższej ankiecie wprowadźcie dane pierwszego z nich.
                Po wysłaniu pierwszej ankiety pojawi się możliwość wysłania drugiej ankiety, 
                potem trzeciej itd.
            </div>
        </div>

        <h4 class="mt-4">Dane pojazdu</h4>
        <SelectCongregation />

        <div class="mt-3">
            <label class="form-label">Typ pojazdu</label>
            <select class="form-select">
                <option value="minibus_30">Minibus do 30 osób</option>
                <option value="autokar_50" selected>Autokar do 50 osób</option>
                <option value="autokar_70">Autokar 60-70 osób</option>
                <option value="autobus_12m">Autobus miejski - 12m (krótki)</option>
                <option value="autobus_18m">Autobus miejski - 18m (przegubowy)</option>
            </select>
        </div>

        <div class="mt-3">
            <label class="form-label">Zapotrzebowanie parkingowe</label>
            <div class="form-check">
                <input class="form-check-input" type="radio" name="parking" id="p1" />
                <label class="form-check-label" for="p1">Potrzebne miejsce parkingowe dla autokaru / busa</label>
            </div>
            <div class="form-check">
                <input class="form-check-input" type="radio" name="parking" id="p2" checked />
                <label class="form-check-label" for="p2">Autokar / autobus tylko dowozi pasażerów, odjeżdza i przyjeżdza odebrać ich po programie</label>
            </div>
        </div>
    </div>

    <div class="mt-4">
        <h4>Dane kontaktowe zborowego pilota dedykowanego do tego autokaru / autobusu / busa.</h4>

        <div class="form-check">
            <input class="form-check-input" type="checkbox" id="sp" v-model="single_pilot" />
            <label class="form-check-label" for="sp">
                Jeden pilot na wszystkie dni kongresowe
            </label>
        </div>

        <template v-if="single_pilot">
            <div class="mt-3">
                <label class="form-label">Imię</label>
                <input class="form-control" v-model="pilot1.firstname" />
            </div>

            <div class="mt-3">
                <label class="form-label">Nazwisko</label>
                <input class="form-control" v-model="pilot1.lastname" />
            </div>

            <div class="mt-3">
                <label class="form-label">Numer telefonu</label>
                <div class="input-group">
                    <select class="form-select flex-grow-0" style="min-width: 90pt" v-model="pilot1.phone.direct">
                        <option value="+48">PL: +48</option>
                        <option value="+7">RU: +7</option>
                        <option value="+380">UA: +380</option>
                    </select>
                    <input class="form-control" placeholder="Wpisz 9/10 cyfr numeru telefonu" />
                </div>
            </div>

            <div class="mt-3">
                <label class="form-label">Podaj prywatny adres poczty elektronicznej (inny niż w domienie @jwpub.org)</label>
                <input class="form-control" />
            </div>
        </template>
        <template v-else>
            <div>
                TODO: sekcja w przygotowaniu
            </div>
        </template>

    </div>

    <div class="mt-4">
        <h4 class="form-label">Uwagi i dodatkowe informacje</h4>
        <textarea class="form-control" rows="3" />
        <small>
            Uwaga: Nie gwarantujemy preferowanych godzin odjazdu spod stadionu. 
            Postaramy się uzględnić wszelkie uwagi jeśli tylko będzie taka możliwość.            
        </small>
    </div>

    <div class="mt-4">
        <button class="btn btn-outline-primary btn-lg" @click="onSubmit">
            Dalej
        </button>
    </div>    
</template>

<style scoped>
.alert-layout {
    display: flex;
    gap: 6pt;
    align-items: baseline;
    font-size: 0.9rem;
}

.numer-telefonu {
    display: flex;
    flex-direction: row;
    gap: 9pt;
}
</style>