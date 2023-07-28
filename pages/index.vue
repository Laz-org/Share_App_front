<script lang="ts" setup>

import { User } from 'entities';
import { Address } from 'entities';

const username: Ref<string> = ref("billy");

let n_u_number: string = "";
let n_u_street: string = "";
let n_u_city: string = "";
let n_u_country: string = "";
let my_display: Ref<boolean> = ref(true);

async function handleSubmit() {
  try {
    let billy:User | null = await $fetch("http://localhost:8000/api/user/name/" + username.value)
    console.log(billy);
    window.location.href += "/main?" + "id=" + billy?._id;
  } catch (error) {
    hide_button();
    console.log(error);
  }
  return;
}

function hide_button() {
  my_display.value = !my_display.value;
  return;
}

async function create_user() {
  let new_user:User = {name: username.value, address:{number: n_u_number, street: n_u_street, city: n_u_city, country: n_u_country}}

  if (username.value === "" || n_u_city === "" || n_u_country === "" || n_u_number === "" || n_u_street === "") {
    alert("faut completer le formulaire");
    return;
  }
  try {
    await $fetch('http://localhost:8000/api/user/', {
      method: 'POST',
      body: new_user
    });
    handleSubmit();
    return;
  } catch (error) {
    console.log(error);
    return;
  }
}

</script>


<template>
  <div>
    <h3>Welcome !</h3>
  </div>
  <div :class="{ hidden: !my_display }">
    <form @submit.prevent="handleSubmit()">
      <label for="name">entre ton nom</label>
      <input type="text" id="name" v-model="username">
      <input type="submit">
    </form>
  </div>
    <div :class="{ hidden: my_display }">
      <p>Connais pas, tu veut creer un compte?</p>

      <label for="nb">number:</label>
      <input type="text" id="nb" v-model="n_u_number">
      <br>

      <label for="street">street:</label>
      <input type="text" id="street" v-model="n_u_street">
      <br>

      <label for="city">city:</label>
      <input type="text" id="city" v-model="n_u_city">
      <br>

      <label for="country">country:</label>
      <input type="text" id="country" v-model="n_u_country">
      <br>

      <button @click="create_user()">oui</button>
      <button @click="hide_button()">nop</button>
    </div>
</template>


<style scoped>
.hidden {
  display: none;
}
</style>