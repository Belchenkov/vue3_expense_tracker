<template>
  <h3>Add new transaction</h3>
  <form id="form" @submit.prevent="onSubmit">
    <div class="form-control">
      <label for="text">Text</label>
      <input
          v-model="text"
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
          v-model="amount"
          type="number"
          id="amount"
          placeholder="Enter amount..."
      />
    </div>
    <button class="btn">Add transaction</button>
  </form>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import { useToast } from 'vue-toastification';

const toast = useToast();

const text = ref('');
const amount = ref(0);

const onSubmit = (): void => {
  if (!text.value || !amount.value) {
    toast.error('Both fields must be filled');
    return;
  }

  text.value = '';
  amount.value = 0;
};
</script>

<style scoped>

</style>
