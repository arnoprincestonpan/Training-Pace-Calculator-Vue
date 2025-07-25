<template>
    <div class="accordion-item">
        <h2 class="accordion-header">
            <button class="accordion-button" type="button" data-bs-toggle="collapse"
                :data-bs-target="`#panelsStayOpen-collapse` + accordionItemId" aria-expanded="true"
                :aria-controls="`panelsStayOpen-collapse` + accordionItemId">
                {{ title }}
            </button>
        </h2>
        <div :id="`panelsStayOpen-collapse` + accordionItemId" class="accordion-collapse collapse"
            v-bind:class="descriptionCollasped ? '' : 'show'">
            <div class="accordion-body">
                {{ description }}
            </div>
        </div>
    </div>
</template>
<script setup>
import { defineProps } from 'vue'
const props = defineProps({
    title: {
        type: String,
        default: "",
    },
    description: {
        type: String,
        default: ""
    },
    descriptionCollasped: {
        type: Function || Boolean,
        default: true,
    },
    accordionItemId: {
        type: Number,
        required: true,
    }
})
</script>