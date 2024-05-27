<script setup>
  import Header from './components/Header.vue'
  import Balance from './components/Balance.vue'
  import incomeExpense from './components/incomeExpenses.vue'
  import transactionList from './components/transactionList.vue'
  import addTransaction from './components/addTransaction.vue'

  import { ref, computed, onMounted} from 'vue';
  import {useToast} from 'vue-toastification'

  const toast = useToast()

  const transactions = ref([]);

  onMounted(() => {
    const storedTransactions = JSON.parse(localStorage.getItem('transactions'));

    if(storedTransactions){
      transactions.value = storedTransactions;
    }
  })

  //get total
  const total = computed(() => {
    return transactions.value.reduce((acc, item) => (acc += item.amount), 0).toFixed(2);
  })

  //get credit
  const credit = computed(() => {
    return transactions.value
    .filter((transaction) => transaction.amount > 0)
    .reduce((acc, item) => (acc += item.amount), 0).toFixed(2);
  })


  //get debit
  const debit = computed(() => {
    return transactions.value
    .filter((transaction) => transaction.amount < 0)
    .reduce((acc, item) => (acc += item.amount), 0).toFixed(2);
  });

  

  //add transaction

  const handleTransactionSubmitted = (transactionData) => {
    const generatedId = transactions.value.length + 1;
    transactions.value.unshift({
      id : generatedId,
      text : transactionData.text,
      amount : transactionData.amount
    })
    storeTransactionsToLocalStorage();
    toast.success('Transaction added successfully')
  }

  //delete transaction
  const handleTransactionDeleted = (id) => {
    transactions.value = transactions.value.filter(transaction => transaction.id !== id);
    storeTransactionsToLocalStorage();
    toast.success('Transaction deleted successfully')
  }

  //store transactions
  const storeTransactionsToLocalStorage = () => {
    localStorage.setItem('transactions', JSON.stringify(transactions.value))
  }


</script>

<template>
  <Header />
  <Balance :total="+total"/>
  <incomeExpense :credit="+credit" :debit="+debit"/>
  <transactionList :transactions="transactions" @transactionDeleted="handleTransactionDeleted"/>
  <addTransaction @transactionSubmitted="handleTransactionSubmitted"/>
</template>

