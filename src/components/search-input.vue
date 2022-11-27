<script setup lang="ts">
import { useStore } from '@/store';
const store = useStore();
</script>

<template>
  <input
  class="input"
    placeholder="введите адрес или номер машины"
    type="text"
    :value="store.state.search"
    @input="(e) => store.commit('SET_SEARCH', e.target.value)"
  />
</template>

<style scoped>
  .input{
    max-width: 15%;
    min-width: 250px;
    height: 30px;
    color: rgb(36, 35, 35);
    border: 0.5px solid lightgray;
    text-align: center;
    border-radius: 5px;
    box-shadow: rgba(253, 253, 253, 0.5px);
  }
  .input :hover{
    color: black;
  }
</style>