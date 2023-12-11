<template>
  <h3>History</h3>
  <ul id="list" class="list">
    <li
        v-for="tr in transactions"
        :key="tr.id"
        :class="tr.amount < 0 ? 'minus' : 'plus'"
    >
      {{ tr.text }} <span>${{ tr.amount }}</span>
      <button class="delete-btn" @click.prevent="deleteTransaction(tr.id)">
        <img width="35" height="35" src="https://img.icons8.com/plasticine/100/trash--v1.png" alt="trash--v1"/>
      </button>
    </li>
  </ul>
</template>

<script lang="ts" setup>
import { defineEmits, defineProps, PropType, ref } from 'vue';

  const props = defineProps({
    transactions: {
      type: Array as PropType<ref<ITransaction>>,
      required: true,
    }
  });

  const emit = defineEmits(['transactionDeleted']);

  const deleteTransaction = (id: number): void => {
    emit('transactionDeleted', id);
  };
</script>
