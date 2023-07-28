<script lang="ts" setup>


const route = useRoute();
let user_id = route.query.id;

</script>

<template>
  <div>

    <h2>tes items:</h2>
    <my_list-item :user_id="user_id"/>

    <h2>les emprunts</h2>
    <list-loan_request :user_id="user_id"/>

    <h2>tes emprunts actuels</h2>
    <my_list-loan_request :user_id="user_id"/>

  </div>
</template>

<style scoped></style>