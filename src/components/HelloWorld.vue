<template>
  <h1>{{ msg }}</h1>

  <h2>My Name is {{state.name}}</h2>
<qr :value="state.name"></qr>
  <p class="">Are you into Crypto 🤑 I have got the latest price for you 😉  </p>

</template>

<script setup>
import { defineProps, reactive } from 'vue'
import qr from './qr.vue'

defineProps({
  msg: String
  
})

const state = reactive({ name: "Adeoye Adela"})

</script>

<style scoped>
a {
  color: #42b983;
}

</style>
