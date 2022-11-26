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

  <SearchInput />
  <div v-if="isDateDefined">
    <MachinesList />
  </div>
</template>

<style scoped></style>