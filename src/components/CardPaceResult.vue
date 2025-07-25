<template>
    <div class="card" style="width: auto">
        <div class="card-header">
            {{ title }}
        </div>
        <ul class="list-group list-group-flush">
            <li class="list-group-item">{{ item }}</li>
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