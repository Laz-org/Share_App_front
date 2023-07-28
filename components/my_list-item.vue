<script lang="ts" setup>

import { Item } from 'entities';

 const props = defineProps<{user_id: string}>();
const {data: items, refresh} = await useFetch<Item[]>('http://localhost:8000/api/item/');

async function fct_item(item:Item) {
    refresh();
}

</script>

<template>
  <my_list_i_did :user_id="user_id"/>
  <div>
    <h3>tous les items</h3>
    <span v-for="elem of items">
    <single-item :sg_item="elem" />
    </span>
  </div>
</template>

<style scoped></style>
