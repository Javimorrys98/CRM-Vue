<script setup>
import { RouterLink } from 'vue-router';

const props = defineProps({
    to: {
        type: String,
        required: true
    }
})
</script>

<template>
    <RouterLink :to="{ name: to }" class="block md:inline-block rounded bg-blue-600 py-2 px-3 font-bold text-white uppercase text-sm shadow hover:bg-blue-500">
    <slot></slot>
    </RouterLink>
</template>
