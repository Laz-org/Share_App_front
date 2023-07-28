<script lang="ts" setup>

import { Item } from 'entities';
import { User } from 'entities';

const props = defineProps<{sg_item: Item}>();

let usr: User | null = await $fetch("http://localhost:8000/api/user/" + props.sg_item.id_owner);
console.log(props.sg_item.id_owner);

</script>

<template>
  <div>
    <p>{{ sg_item.item_name }}</p>
    <p v-if="!sg_item.available">indisponible</p>
    <p>type: {{ sg_item.type }}</p>
    <span v-if="usr !== null">
      <p>owner: {{ usr.name }}</p>
    </span>
  </div>
</template>

<style scoped></style>
