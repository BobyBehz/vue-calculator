<template>
    <button @click="emit('operate')" class="w-full aspect-square">
        {{ operator }}
    </button>
</template>

<script setup>
const props = defineProps({
    operator: Object
})
const emit = defineEmits([
    'operate',
])
</script>
