<script lang="ts" setup>

import { Loan_Request } from 'entities';

const props = defineProps<{user_id: string}>();
const {data:loans, refresh} = await useFetch<Loan_Request[]>('http://localhost:8000/api/loan_request/');

async function fct_my_loan(loan:Loan_Request) {
    refresh();
}

</script>

<template> 
  <div>
    <h4>tous les prets</h4>
    <span v-for="elem of loans">
    <single-loan_request :sg_loan="elem" />
    </span>
  </div>
</template>

<style scoped></style>
