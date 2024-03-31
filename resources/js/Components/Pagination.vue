<script setup>
import { Link } from '@inertiajs/vue3'

defineProps({
    links: {
        type: Array,
        required: true,
    },
});
</script>


<template>
    <nav class="text-center mt-4">
        <Link v-for="link in links" :key="link.label" :href="link.url || ''" :class="{
            'inline-block py-2 px-3 rounded-lg text-gray-200 text-xs': true,
            'bg-gray-950': link.active,
            '!text-gray-500 cursor-not-allowed': !link.url,
            'hover:bg-gray-950': link.url,
        }" :preserve-scroll="true" v-html="link.label" />
    </nav>
</template>
