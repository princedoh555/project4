<script setup>
    import {ref, defineEmits} from 'vue'
    const text = ref('')
    const amount = ref('')

    const emit = defineEmits([
        'purchaseSubmitted'
    ])

    const onSubmit = () =>{
        const purchaseData = {
            text: text.value,
            amount: parseFloat(amount.value),
        }

        emit('purchaseSubmitted', purchaseData)

        text.value = ''
        amount.value = ''
    }


</script>

<template>
    <h3>Add a new Purchase</h3>
    <form id="form" @submit.prevent="onSubmit">
        <div class="form-control">
            <label for="text">Enter Purchase</label>
            <input type="text" id="text" v-model="text" placeholder="Enter Purchase...">
        </div>
        <div class="form-control">
            <label for="amount">Enter Purchase Amount</label>
            <input type="text" id="amount" v-model="amount" placeholder="Enter Negative Value for Expenses">
        </div>
        <button class="btn">Add Purchase</button>
    </form>
</template>