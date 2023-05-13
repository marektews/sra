<script setup>
import { ref, watch, computed, onBeforeUnmount } from 'vue'

const hints = ref([])
const ops = ref(null)

const name = computed({
    get() {
        return props.modelValue
    },
    set(value) {
        emit('update:modelValue', value)
        isFinished(value)
    }
})

const props = defineProps(['modelValue'])

const emit = defineEmits(['update:modelValue', 'finished'])

watch(name, async (value, old) => {
    // console.log("Watcher:", value, old)
    if(value.length < 3) {
        hints.value = []
        return
    }

    if(Math.abs(value.length - old.length) === 1) {
        if(ops.value) clearTimeout(ops.value)
        ops.value = setTimeout(getHints, 500)
    }
})

async function getHints() {
    try {
        const res = await fetch(`/api/srp/congregations/search/${name.value}`)
        if(res.status === 200) {
            hints.value = await res.json()
            isFinished(name.value)
        }
    }
    catch(e) {
        console.debug(e)
    }
}

onBeforeUnmount(() => {
    if(ops.value) clearTimeout(ops.value)
})

function isFinished(value) {
    let b = hints.value.length == 1 && hints.value.includes(value)
    emit('finished', b)
}
</script>

<template>
    <div>
        <input 
            v-model="name"
            type="text" 
            class="form-control form-select-lg"
            list="hints"
            title="Wpisz 3 znaki, a pojawi się lista podpowiedzi ułatwiająca wybór"
            placeholder="Wpisz 3 znaki, a pojawi się lista podpowiedzi ułatwiająca wybór"
        />

        <datalist id="hints">
            <option v-for="(item, index) in hints" :value="item" :key="index" />
        </datalist>       
    </div>
</template>