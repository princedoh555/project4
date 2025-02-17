<script setup>
    import {defineProps} from 'vue'

    const props = defineProps({
        total: {
            type: Number,
            require: true,
        }
    })


</script>


<template>
    <h4>Your Receipt</h4>
    <h1 id="receipt">{{ total }}</h1>


</template>