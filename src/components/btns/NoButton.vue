<template>
    <button class="btn btn-lg btn-outline-danger">
        <FontAwesomeIcon :icon="faCircleXmark" />
        <span class="ms-2">NIE</span>
    </button>
</template>

<script setup>
import { FontAwesomeIcon } from '@fortawesome/vue-fontawesome';
import { faCircleXmark } from '@fortawesome/free-solid-svg-icons';
</script>