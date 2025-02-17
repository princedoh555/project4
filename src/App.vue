<script setup>
  import Header from './components/Title.vue';
  import Total from './components/Total.vue';
  import IncomeExpense from './components/IncomeExpense.vue';
  import AddPurchase from './components/AddPurchase.vue';
  import PurchaseList from './components/PurchaseList.vue';

  import {ref, computed, onMounted} from 'vue'

  const purchase = ref([])

  const sum = computed(()=>{
    return purchase.value.reduce((acc, x)=>{
      return acc+x.amount
    },0)
  })

  const moneyIn = computed(()=>{
    return purchase.value
    .filter((x)=>x.amount>0)
    .reduce((acc, x)=>{
      return acc+x.amount
    },0)
  })

  const moneyOut = computed(()=>{
    return purchase.value
    .filter((x)=>x.amount<0)
    .reduce((acc, x)=>{
      return acc+x.amount
    },0)
  })

  const handlePurchase = (purchaseData) =>  {
    purchase.value.push({
      id: generateID(),
      text: purchaseData.text,
      amount: purchaseData.amount,
    })
    saveToLocalStorage()
  }

  const generateID = () =>{
    return Math.floor(Math.random()*20000000)
  }

  const handleDelete = (id) => {
    purchase.value = purchase.value.filter((x) => x.id !== id)
    saveToLocalStorage()
  }

  const saveToLocalStorage = () => {
    localStorage.setItem('purchase', JSON.stringify(purchase.value))
  }

  onMounted( () => {
    const savedpurchase = JSON.parse(localStorage.getItem('purchase'))

    if(savedPurchase){
      purchase.value = savedPurchase
    }
  })

</script>


<template>
  <Header></Header>
  <div class="container">
    <Total :total="sum"></Total>
    <IncomeExpense :income="moneyIn" :expense="moneyOut"></IncomeExpense>
    <AddPurchase @purchaseSubmitted="handlePurchase"></AddPurchase>
    <PurchaseList :purchase="purchase" @purchaseDeleted="handleDelete"></PurchaseList>
  </div>

</template>