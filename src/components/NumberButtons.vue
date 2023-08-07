<template>
    <button @click="emit('put')"
        class="w-full aspect-square">
        {{ number }}
    </button>
</template>

<script setup>
const props = defineProps({
    number: Object
})
const emit = defineEmits([
    'put',
])
</script>