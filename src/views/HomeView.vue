<script setup lang="ts">
  import Header from '../components/Header.vue';
  import Balance from '../components/Balance.vue';
  import IncomeExpense from '../components/IncomeExpense.vue';
  import TransactionList from '../components/TransactionList.vue';
  import AddTransaction from '../components/AddTransaction.vue';
</script>

<template>
  <header>
    <Header />
  </header>
  <main>
    <div class="container">
      <Balance />
      <IncomeExpense />
      <TransactionList />
      <AddTransaction />
    </div>
  </main>
</template>
