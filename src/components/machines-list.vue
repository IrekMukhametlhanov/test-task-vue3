<script setup lang="ts">
import MachineItem from './machine-item.vue';
import { useStore } from '@/store';
import { computed, ref, watch } from 'vue';
import type { IMachine } from '@/interfaces/machine.interface';
const store = useStore();
const filteredMachines = ref<IMachine[]>([]);
const machines = computed(() => store.state.machines);
watch(
  () => store.state.search,
  () => {
    filteredMachines.value = store.getters.filteredMachines;
  }
);
</script>

<template>
  <div class="wrap">

    <div class="machine-wrapper">
    <ul v-if="!store.state.search">
      <li :key="machine" v-for="machine in machines">
        <MachineItem :id="machine.id" />
      </li>
    </ul>
    <ul v-else>
      <li :key="machine" v-for="machine in filteredMachines">
        <MachineItem :id="machine.id" />
      </li>
    </ul>
  </div>
  </div>
</template>
<style scoped>
 .wrap{
  max-width: 70vw;
  max-height: 70vh;
  margin: 0 auto;

 }
 .machine-wrapper{
  max-width: 70vw;
  margin: 0 auto;
  max-height: 80vh;
  /* background-color: lightgray; */
  overflow-y: auto;
 }

 li{
  list-style-type: none;
 }
 .machines-list{
   color: yellowgreen;
 }

 ::-webkit-scrollbar{
    width: 10px;
}

::-webkit-scrollbar-track{
    background:rgb(255, 255, 255) ;
}

::-webkit-scrollbar-thumb{
    background: linear-gradient(to bottom, rgb(87, 87, 87),rgb(104, 104, 104));
    border-radius: 8px;
    border: 3px solid rgb(249, 249, 250);
}
    

.view-change{
    position: absolute;
    font-size: large;
    z-index: 100;
    cursor: pointer;
    text-align: center;
    padding-top: 8px;
    width: 48px;
    color: rgb(0,9,7);
    height: 48px;
    border: 2px solid rgb(108, 108, 108);
    border-radius: 10px;
    margin-left: 60%;
}
</style>
