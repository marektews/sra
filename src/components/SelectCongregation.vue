<script setup>
import { ref, watch } from 'vue'

const name = ref('')
const hints = ref([])

const emit = defineEmits(['congregation'])

watch(name, async (value, old) => {
    // console.log("Watcher:", value, old)
    if(value.length < 3) {
        hints.value = []
        return
    }

    if(Math.abs(value.length - old.length) === 1) {
        try {
            const res = await fetch(`/api/srp/congregations/search/${value}`)
            hints.value = await res.json()
        }
        catch(e) {
            console.debug(e)
        }
    }
    else {
        if(hints.value.includes(name.value)) {
            emit('congregation', name.value)
        }
    }
})

</script>

<template>
    <div>
        <label class="form-label">Nazwa zboru</label>
        
        <input 
            v-model="name"
            type="text" 
            class="form-control"
            list="hints"
            placeholder="Wpisz przynajmniej 3 znaki, a pojawi się lista podpowiedzi ułatwiająca wybór"
        />

        <datalist id="hints">
            <option v-for="(item, index) in hints" :value="item" :key="index" />
        </datalist>       
    </div>
</template>