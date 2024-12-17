<script lang="ts" setup>
defineProps({
    label: {
        type: String,
        required: true
    },
    value: {
        type: [String, Number, Object],
        required: true
    },
    valueSecond: {
        type: String,
        required: false
    }
})
</script>
<template>
    <div class="font-medium">
        <h1 class="font-medium">{{ label }}</h1>
        <h4 class="font-normal">{{ value }}</h4>
        <h4 class="font-normal">{{ valueSecond }}</h4>
    </div>
</template>
