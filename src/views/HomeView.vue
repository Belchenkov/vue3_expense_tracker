<template>
  <header>
    <Header />
  </header>
  <main>
    <div class="container">
      <Balance :total="total" />
      <IncomeExpense :income="income" :expenses="expenses" />
      <TransactionList
          :transactions="transactions"
          @transactionDeleted="handleTransactionDeleted"
      />
      <AddTransaction @transactionSubmitted="handleTransactionSubmitted" />
    </div>
  </main>
</template>

<script setup lang="ts">
import { ref, computed, onMounted } from 'vue';
import { useToast } from 'vue-toastification';

import Header from '../components/Header.vue';
import Balance from '../components/Balance.vue';
import IncomeExpense from '../components/IncomeExpense.vue';
import TransactionList from '../components/TransactionList.vue';
import AddTransaction from '../components/AddTransaction.vue';

const toast = useToast();

// const transactions: ref<ITransaction[]> = ref([
//   { id: 1, text: 'Flower', amount: -19.99 },
//   { id: 2, text: 'Salary', amount: 299.99 },
//   { id: 3, text: 'Book', amount: -10.99 },
//   { id: 4, text: 'Camera', amount: 150 },
// ]);

const transactions: ref<ITransaction[]> = ref([]);

const total = computed((): number => {
  return transactions.value.reduce((acc: number, tr: ITransaction) => {
    return acc + tr.amount;
  }, 0);
});

const income = computed((): string => {
  return transactions.value
      .filter((tr: ITransaction) => tr.amount > 0)
      .reduce((acc: number, tr: ITransaction) => {
    return acc + tr.amount;
  }, 0)
      .toFixed(2);
});

const expenses = computed((): string => {
  return transactions.value
      .filter((tr: ITransaction) => tr.amount < 0)
      .reduce((acc: number, tr: ITransaction) => {
    return acc + tr.amount;
  }, 0)
      .toFixed(2);
});

const handleTransactionSubmitted = (newTrData: IAddTransaction): void => {
  transactions.value.push({
    id: generateUniqueId(),
    text: newTrData.text,
    amount: newTrData.amount,
  });

  saveTransactionsToLocalStorage();

  toast.success('Transaction added!');
};

const handleTransactionDeleted = (id: number) => {
  transactions.value = transactions.value.filter((tr: ITransaction) => tr.id !== id);

  saveTransactionsToLocalStorage();

  toast.success('Transaction deleted!');
};

const saveTransactionsToLocalStorage = (): void => {
  localStorage.setItem('transactions', JSON.stringify(transactions.value));
};

const generateUniqueId = (): number => {
  return Math.floor(Math.random() * 1000000);
};

onMounted((): void => {
  const savedTransactions = JSON.parse(localStorage.getItem('transactions'));

  if (savedTransactions) {
    transactions.value = savedTransactions;
  }
});

</script>
