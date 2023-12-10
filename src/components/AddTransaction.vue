<template>
  <h3>Add new transaction</h3>
  <form id="form" @submit.prevent="onSubmit">
    <div class="form-control">
      <label for="text">Text</label>
      <input
          v-model.trim="text"
          type="text"
          id="text"
          placeholder="Enter text..."
      />
    </div>
    <div class="form-control">
      <label for="amount"
      >Amount <br />
        (negative - expense, positive - income)</label
      >
      <input
          v-model.number="amount"
          type="number"
          id="amount"
          placeholder="Enter amount..."
      />
    </div>
    <button class="btn">Add transaction</button>
  </form>
</template>

<script setup lang="ts">
import { defineEmits, ref } from 'vue';
import { useToast } from 'vue-toastification';

const toast = useToast();
const emit = defineEmits(['transactionSubmitted']);

const text = ref('');
const amount = ref(0);

const onSubmit = (): void => {
  if (!text.value || !amount.value) {
    toast.error('Both fields must be filled');
    return;
  }

  emit('transactionSubmitted', {
    text: text.value,
    amount: amount.value,
  });

  text.value = '';
  amount.value = 0;
};
</script>

<style scoped>

</style>
