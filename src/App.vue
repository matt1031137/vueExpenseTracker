<template>
  <Header />
  <div class="container">
    <Balance :total="total" />
    <IncomeExpense :income="income" :expense="expense" />
    <TransactionList :transactions="transactions" @delete="deleteItem" />
    <AddTransaction @addTransactions="addList" />
  </div>
</template>


<script setup>
import Header from './components/Header.vue'
import Balance from './components/Balance.vue'
import IncomeExpense from './components/IncomeExpense.vue'
import TransactionList from './components/TransactionList.vue'
import AddTransaction from './components/AddTransaction.vue'

import { ref, computed, onMounted } from 'vue'
import { useToast } from 'vue-toastification'

const transactions = ref([])

const toast = useToast()

//刪除
const deleteItem = (id) => {
  transactions.value = transactions.value.filter((item) => item.id != id)
  saveTransactionsToLocalStorage()
  toast.success('刪除成功!')
}

//追加
const addList = (data) => {
  transactions.value.push({ ...data, id: generateUniqueId() })
  saveTransactionsToLocalStorage()
  console.log(transactions.value)

}

//總計
const total = computed(() => {
  return transactions.value.reduce((acc, transaction) => (
    acc + transaction.amount
  ), 0)
})

//收入
const income = computed(() => {
  return transactions.value
    .filter((transaction) => transaction.amount > 0)
    .reduce((acc, transaction) => (
      acc + transaction.amount
    ), 0)

  //教學影片有教到.tofixed(2) 取到小數點第二位，但台幣都整數所以不需要
})


//支出
const expense = computed(() => {
  return transactions.value
    .filter((transaction) => transaction.amount < 0)
    .reduce((acc, transaction) => (
      acc + transaction.amount
    ), 0)

  //教學影片有教到.tofixed(2) 取到小數點第二位，但台幣都整數所以不需要
})



const generateUniqueId = () => {
  return Math.floor(Math.random() * 10000)
}

//儲存localStorage
const saveTransactionsToLocalStorage = () => {
  localStorage.setItem('transactions', JSON.stringify(transactions.value))
}

onMounted(() => {
  const saveTransactions = JSON.parse(localStorage.getItem('transactions'))

  if (saveTransactions) {
    transactions.value = saveTransactions
  }
})

</script>
