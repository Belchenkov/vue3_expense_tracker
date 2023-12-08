<template>
  <h3>History</h3>
  <ul id="list" class="list">
    <li
        v-for="tr in transactions"
        :key="tr.id"
        :class="tr.amount < 0 ? 'minus' : 'plus'"
    >
      {{ tr.text }} <span>${{ tr.amount }}</span>
    </li>
  </ul>
</template>

<script lang="ts" setup>
  import { defineProps } from 'vue';

  const props = defineProps({
    transactions: {
      type: Array,
      required: true,
    }
  });
</script>
