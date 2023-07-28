<script lang="ts" setup>

import { Item } from 'entities';

const props = defineProps<{user_id: string}>();
let o_name: string = "";
let o_type: string = "";
let o_avail: string = "";
let o_ava: boolean = false;

async function form_finished() {
  if (o_name == "" || (o_type != "animal" && o_type != "equipement" && o_type != "autre") || (o_avail != "o" && o_avail != "n" )) {
    alert("faut completer le formulaire correctement");
    return;
  }
  if (o_avail == "o") {
    o_ava = true;
  }
  let new_item: Item = {item_name:o_name, type:o_type, available:o_ava, id_owner:props.user_id};
  try {
    await $fetch('http://localhost:8000/api/item/', {
      method: 'POST',
      body: new_item
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
    <form @submit.prevent="form_finished()">
      <label for="name">entre le nom de ton objet</label>
      <input type="text" id="name" v-model="o_name">

      <label for="type">quel est son type entre animal, equipement et autre</label>
      <input type="text" id="type" v-model="o_type">
      
      <label for="ava">est il disponible o/n</label>
      <input type="text" id="ava" v-model="o_avail">

      <input type="submit">
    </form>
  </div>
</template>

<style scoped></style>
