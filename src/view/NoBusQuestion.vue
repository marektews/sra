<template>
    <div class="container">
        <div class="layout">
            <h4>
                Czy zbór planuje dojazd autokarem?
            </h4>

            <div class="mt-4">
                <YesButton @click="onYesClicked" />
                <NoButton class="ms-2" @click="onNoClicked" />
            </div>
        </div>
    </div>
</template>

<script setup>
import YesButton from '@/components/btns/YesButton.vue';
import NoButton from '@/components/btns/NoButton.vue';

const props = defineProps(['congregation'])
const emit = defineEmits(['back', 'next'])
function onYesClicked() {
    emit('next')
}
function onNoClicked() {
    fetch(`/api/sra/submit/nobus/${props.congregation}`, {
        method: "PUT",
    })
    .then(resp => {
        if(resp.ok) {
            console.log("No bus registration OK")
        } 
        else {
            console.error("No bus registration error status:", resp.status, resp.statusText)
        }
    })
    .catch(err => console.error("No bus registration error:", err))
    emit('finished')
}

</script>

<style lang="css" scoped>
.layout {
    display: flex;
    flex-direction: column;
    align-items: center;
}
</style>