<script lang="ts" setup>

import { Loan_Request } from 'entities';

const props = defineProps<{sg_loan: Loan_Request}>();

</script>

<template>
  <div>
    <p>{{ sg_loan.message }}</p>
    <p v-if="sg_loan.pending">en attente</p>
    <p>start loan: {{ sg_loan.start_loan_date }}</p>
    <p>end loan: {{ sg_loan.end_loan_date }}</p>
  </div>
</template>

<style scoped>
div {
  background-color: rgb(198, 241, 200);
}
</style>
