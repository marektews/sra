<script setup>
import { reactive, computed } from 'vue'
import FooterButtons from '@/components/btns/FooterButtons.vue'
import TitleView from '@/components/TitleView.vue'

const props = defineProps(['modelValue'])
const bus = reactive(props.modelValue)

const emit = defineEmits(['update:modelValue', 'back', 'next'])
function onNextClicked() {
    emit('next')
}
function onBackClicked() {
    emit('back')
}

function onTypeChanged(e) {
    bus.type = e.target.value
    emit('update:modelValue', bus)
}

function onDistanceChanged(e) {
    bus.distance = e.target.value
    emit('update:modelValue', bus)
}

function onP1Changed(e) {
    if(e.target.value) {
        bus.parking_mode = 'needed'
        emit('update:modelValue', bus)
    }
}
function onP2Changed(e) {
    if(e.target.value) {
        bus.parking_mode = 'not_needed'
        emit('update:modelValue', bus)
    }
}

const isNextBtnEnabled = computed(() => {
    return bus.type.length > 0 && bus.distance.length > 0
})
</script>

<template>
    <div>
        <TitleView>
            Dane autokaru / autobusu / busa
        </TitleView>
        
        <div class="mb-4">
            <label class="form-label">Typ pojazdu</label>
            <select class="form-select form-select-lg" 
                :value="bus.type" 
                @input="onTypeChanged($event)"
            >
                <option value="minibus_30">Minibus do 30 osób</option>
                <option value="autokar_50">Autokar do 50 osób</option>
                <option value="autokar_70">Autokar 60-70 osób</option>
                <option value="autobus_12m">Autobus miejski - 12m (krótki)</option>
                <option value="autobus_18m">Autobus miejski - 18m (przegubowy)</option>
            </select>
        </div>

        <div class="mb-4">
            <label class="form-label">Długość trasy</label>
            <select class="form-select form-select-lg"
                :value="bus.distance"
                @input="onDistanceChanged($event)"
            >
                <option value="10km">do 10 km</option>
                <option value="20km">do 20 km</option>
                <option value="50km">do 50 km</option>
                <option value="100km">do 100 km</option>
                <option value="more100km">powyżej 100 km</option>
            </select>
        </div>

        <div>
            <label class="form-label">Zapotrzebowanie parkingowe</label>
            <div class="form-check">
                <input class="form-check-input" type="radio" name="parking" id="p1" 
                    :checked="bus.parking_mode === 'needed'"
                    @input="onP1Changed($event)"
                />
                <label class="form-check-label" for="p1">Potrzebne miejsce parkingowe dla autokaru / busa</label>
            </div>
            <div class="form-check">
                <input class="form-check-input" type="radio" name="parking" id="p2" 
                    :checked="bus.parking_mode === 'not_needed'"
                    @input="onP2Changed($event)"
                />
                <label class="form-check-label" for="p2">Autokar / autobus tylko dowozi pasażerów, odjeżdza i przyjeżdza odebrać ich po programie</label>
            </div>
        </div>

        <FooterButtons
            @next="onNextClicked"
            @back="onBackClicked"
            :next-enabled="isNextBtnEnabled"
        />

    </div>
</template>