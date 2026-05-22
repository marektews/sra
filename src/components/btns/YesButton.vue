<template>
    <button class="btn btn-lg btn-outline-success">
        <FontAwesomeIcon :icon="faCircleCheck" />
        <span class="ms-2">TAK</span>
    </button>
</template>

<script setup>
import { FontAwesomeIcon } from '@fortawesome/vue-fontawesome';
import { faCircleCheck } from '@fortawesome/free-solid-svg-icons';
</script>