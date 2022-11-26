<script setup lang="ts">
import MachineItem from './machine-item.vue';

import { onBeforeMount, ref } from 'vue';
import type { IMachine } from '../interfaces/machine.interface';
import { getMachines } from '../services/machines.service';

const machines = ref<IMachine[]>();

onBeforeMount(async () => {
  machines.value = await getMachines();
});
</script>

<template>
  <div class="wrap">
    <h1 class="title">Список кофемашин</h1>
  <div class="machine-wrapper">
  <div class="machines-list">
    <ul>
      <li :key="machine" v-for="machine in machines">
        <MachineItem :machine="machine" />
      </li>
    </ul>
  </div>
</div>
</div>

</template>

<style scoped>
 .wrap{
  max-width: 90vw;
  max-height: 80vh;
  margin: 0 auto;
    ;

 }
 .machine-wrapper{
  max-width: 80vw;
  margin: 0 auto;
  max-height: 70vh;
  background-color: lightgray;
  border: 1px solid black;
  overflow-y: auto;
 }
 .machines-list{
   color: yellowgreen;
 }

 ::-webkit-scrollbar{
    width: 15px;
}

::-webkit-scrollbar-track{
    background:rgb(237, 237, 237) ;
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
