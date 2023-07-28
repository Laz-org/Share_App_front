<script lang="ts" setup>

import { Item } from 'entities';
import { User } from 'entities';

const props = defineProps<{sg_item: Item}>();

const route = useRoute();
let user_id = route.query.id;

let usr: User | null = await $fetch("http://localhost:8000/api/user/" + props.sg_item.id_owner);

async function my_own_delete() {
  try {
    await $fetch('http://localhost:8000/api/item/' + props.sg_item._id, {
      method: 'DELETE'
    });
  } catch (error) {
    console.log(error);
  }
  refreshNuxtData();
  return;
}

</script>

<template>
  <div>
    <p>{{ sg_item.item_name }}</p>
    <p v-if="!sg_item.available">indisponible</p>
    <p>type: {{ sg_item.type }}</p>
    <span v-if="usr !== null">
      <p>owner: {{ usr.name }}</p>
    </span>
    <button v-if="user_id == sg_item.id_owner" @click="my_own_delete()">By Fire Be Purged !!</button>
  </div>
</template>

<style scoped></style>
