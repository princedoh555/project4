<script setup>
    import {defineProps, defineEmits} from 'vue'

    const props = defineProps({
        purchase: {
            type: Array,
            require: true,
        }
    })

    const emit = defineEmits(['purchaseDeleted'])

    const deletePurchase = (id) => {
        emit('purchaseDeleted', id)
    }

</script>

<template>
    <h3>Details</h3>
    <ul id="list" class="list">
        <li v-for="x in purchase" v-bind:key="x.id"
        v-bind:class="x.amount < 0 ? 'minus' : 'plus'">
        {{ x.text }} <span> ${{ x.amount }}</span>
        <button @click="deletePurchase(x.id)" class="delete-button">X</button>
        </li>
    </ul>
</template>