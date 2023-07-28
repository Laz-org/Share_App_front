<script lang="ts" setup>

import { Item } from 'entities';

const props = defineProps<{user_id: string}>();
const {data: my_items, refresh} = await useFetch<Item[]>('http://localhost:8000/api/item/owner/' + props.user_id);

</script>

<template>
  <div>
    <h3>tes items</h3>
    <span v-for="elem of my_items">
      <single-item :sg_item="elem" />
    </span>
    <form-item :user_id="user_id" />
  </div>
</template>

<style scoped></style>
