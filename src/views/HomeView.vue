<template>
  <header>
    <Header />
  </header>
  <main>
    <div class="container">
      <Balance :total="total" />
      <IncomeExpense />
      <TransactionList :transactions="transactions" />
      <AddTransaction />
    </div>
  </main>
</template>

<script setup lang="ts">
import { ref, computed } from 'vue';

import Header from '../components/Header.vue';
import Balance from '../components/Balance.vue';
import IncomeExpense from '../components/IncomeExpense.vue';
import TransactionList from '../components/TransactionList.vue';
import AddTransaction from '../components/AddTransaction.vue';

const transactions: ref<ITransaction[]> = ref([
  { id: 1, text: 'Flower', amount: -19.99 },
  { id: 2, text: 'Salary', amount: 299.99 },
  { id: 3, text: 'Book', amount: -10.99 },
  { id: 4, text: 'Camera', amount: 150 },
]);

const total = computed(() => {
  return transactions.value.reduce((acc: number, tr: ITransaction) => {
    return acc + tr.amount;
  }, 0);
});

</script>
