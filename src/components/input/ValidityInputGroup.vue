<script setup>
import {ref, computed, onMounted} from 'vue'

const valid = ref(null)
const inputCtrl = ref(null)

const props = defineProps({
    modelValue: { type: Object },
    title: { type: String, default: "" },
    type: { type: String, default: "text" },
    maxLength: { type: String, default: "" },
    placeholder: { type: String, default: "" },
    pattern: { type: [String, undefined], default: undefined },
    validFeedback: { type: String, default: "" },
    invalidFeedback: { type: String, default: "" },
    required: { type: Boolean, default: false },
})

const emit = defineEmits(['update:modelValue', 'valid'])

const onBlur = (e) => {
    valid.value = e.target.checkValidity()
    emit('valid', valid.value)

    if(!valid.value) {
        e.target.reportValidity()
    }
}

const validityClass = computed(() => {
    if(valid.value === true) return "is-valid"
    if(valid.value === false) return "is-invalid"
    return ""
})

onMounted(() => {
    if(inputCtrl.value.checkValidity()) {
        valid.value = true
        emit('valid', valid.value)
    }
})
</script>

<template>
    <div>

        <label v-if="title.length"
            class="form-label"
        >
            {{ props.title }}
        </label>

        <input ref="inputCtrl"
            class="form-control form-control-lg"
            :class="validityClass"
            :type="props.type"
            :maxlength="maxLength"
            :placeholder="props.placeholder"
            :pattern="props.pattern"
            :required="props.required"

            :value="props.modelValue"
            @input="$emit('update:modelValue', $event.target.value)"

            @blur="onBlur($event)"
        />

        <template v-if="validFeedback">
            <div v-if="valid" class="valid-feedback">
                {{ validFeedback }}
            </div>
        </template>
        
        <template v-if="invalidFeedback">
            <div v-if="!valid" class="invalid-feedback">
                {{ invalidFeedback }}
            </div>
        </template>

    </div>
</template>