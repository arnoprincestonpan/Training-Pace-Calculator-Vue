<template>
    <div class="card" style="width: auto">
        <div class="card-header">
            {{ props.title }}
        </div>
        <ul class="list-group list-group-flush">
            <li class="list-group-item">{{ props.item }}</li>
        </ul>
    </div>
</template>
<script setup>
import { defineProps } from 'vue';
const props = defineProps({
    title: {
        type: String,
        required: true,
    },
    item: {
        type: String,
        required: true,
    }
})
</script>