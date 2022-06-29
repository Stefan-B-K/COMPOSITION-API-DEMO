<template>
  <section class="container">
    <user-data :user="user"></user-data>
    <button @click="changeAge">Change Age</button>
    <div>
      <input type="text" placeholder="First name" v-model="user.firstName" />
      <input type="text" placeholder="Last name" ref="lastNameInput" />
      <button @click="setlLastName">Set Last Name</button>
    </div>
  </section>
</template>

<script setup>
import { reactive, watch, ref, provide, computed } from 'vue';
import UserData from '@/components/UserData';

const user = reactive({
  firstName: 'Stefan',
  lastName: 'Kozhuharov',
  age: 47
});
const lastNameInput = ref(null);

provide('userLastName', computed(() => user.lastName))

const changeAge = () => user.age += 5;
const setlLastName = () => user.lastName = lastNameInput.value.value;          // .value of DOM input

watch(() => user.age, (newValue, oldValue) => {                                                // pass     '() => user.age '      not    'user.age'
  if (newValue > 100) {
    alert(`Can't let you grow as old as ${newValue}.
You'll remain at the age of ${oldValue} FOREVER`);
    user.age = oldValue;
  }
});


</script>

<style>
* {
  box-sizing: border-box;
}

html {
  font-family: sans-serif;
}

body {
  margin: 0;
}

.container {
  margin: 3rem auto;
  max-width: 30rem;
  border-radius: 12px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
  padding: 1rem;
  text-align: center;
}
</style>