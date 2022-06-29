<template>
  <h2>{{ fullName }}</h2>
  <h3>{{ props.user.firstName }}</h3>
  <h3>{{ lastName }}</h3>
  <h3>{{ props.user.age }}</h3>
</template>


<script  setup>
import { defineProps, computed, inject } from 'vue';

const props = defineProps({ user: Object })

const lastName = inject('userLastName')

const fullName = computed(() => props.user.firstName + ' ' + props.user.lastName)

</script>


<style scoped></style>