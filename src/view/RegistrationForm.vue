<script setup>

const emit =  defineEmits('submit')
const onSubmit = () => {
    emit('submit')
}

</script>

<template>
    <div>
        <h4>Dane pojazdu</h4>
        <div>
            <label class="form-label">Nazwa zboru</label>
            <input class="form-control form-control-lg"  />
        </div>

        <div class="mt-3">
            <label class="form-label">Typ pojazdu</label>
            <select class="form-select form-select-lg">
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
                <label class="form-check-label" for="p1">Potrzebne miejsce parkingowe</label>
            </div>
            <div class="form-check">
                <input class="form-check-input" type="radio" name="parking" id="p2" checked />
                <label class="form-check-label" for="p2">Autokar tylko dowozi i odjeżdza</label>
            </div>
        </div>
    </div>

    <div class="mt-4">
        <h4>Dane kontaktowe pilota</h4>

        <div class="pilot-name">
            <div>
                <label class="form-label">Imię</label>
                <input class="form-control form-control-lg"  />
            </div>

            <div>
                <label class="form-label">Nazwisko</label>
                <input class="form-control form-control-lg"  />
            </div>
        </div>

        <div class="mt-3">
            <label class="form-label">Numer telefonu</label>
            <input class="form-control form-control-lg"  />
        </div>

        <div class="mt-3">
            <label class="form-label">Adres poczty elektronicznej w domenie @jwpub</label>
            <div class="input-group">
                <input class="form-control form-control-lg"  />
                <span class="input-group-text">@jwpub.org</span>
            </div>
        </div>

        <div class="mt-3">
            <label class="form-label">Dodatkowy lub prywatny adres poczty elektronicznej</label>
            <input class="form-control form-control-lg"  />
        </div>
    </div>

    <div class="mt-3">
        <h4 class="form-label">Preferencje odjazdowe</h4>
        <input class="form-control form-control-lg"  />
        <small class="text-muted">
            <div>Uwaga! Nie gwarantujemy preferowanej godziny odjazdu spod stadionu.</div>
            <div>Możemy to uwzględnić, jeśli będzie taka możliwość.</div>
        </small>
    </div>

    <div class="mt-4">
        <h4 class="form-label">Uwagi i dodatkowe informacje</h4>
        <textarea class="form-control form-control-lg" rows="3" />
    </div>

    <div class="mt-4">
        <button class="btn btn-outline-primary btn-lg" @click="onSubmit">
            Wyślij zgłoszenie
        </button>
    </div>    
</template>

<style>
.pilot-name {
    display: flex;
    flex-direction: row;
    gap: 9pt;
}

.pilot-name > div {
    flex-grow: 1;
}
</style>