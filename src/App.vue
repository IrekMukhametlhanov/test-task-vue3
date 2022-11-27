<script setup lang="ts">
import MachinesList from './components/machines-list.vue';
import SearchInput from './components/search-input.vue';
import { computed, onBeforeMount } from 'vue';
import { useStore } from './store';
const store = useStore();
const isDateDefined = computed(
  () =>
    store.state.machines.length &&
    store.state.tradePoints.length &&
    store.state.machineTypes.length
);
onBeforeMount(() => {
  store.dispatch('fetchAll');
});
</script>

<template>
  <div>
  <div class="title_wrapper">
  <h1 class="title">Список кофемашин</h1>
  <SearchInput class="search" />
   </div>
  <div class="machines-list" v-if="isDateDefined">
    <MachinesList />
  </div>
  </div>
</template>

<style scoped>
  .title_wrapper{
    display: flex;
    margin-left: 17vw;
    font-weight: bolder;
    align-items: center;
    text-align: center;
  }

  .title{
    color: rgb(107, 30, 30);
  }
 .search{
  margin-left: 30vw;
 }
 
</style>