<script setup lang="ts">
import type { Schedule } from '../types/schedule.type';

type Props = {
  schedule: Schedule;
};

defineProps<Props>();

defineEmits<{
  (e: 'close'): void;
}>();
</script>

<template>
  <div class="schedule-modal">
    <p class="time">Время работы</p>
    <ul class="ul">
      <li class="li" :key="day" v-for="(value, day) in schedule">
        {{ day }}: {{ value }}
      </li>
    </ul>
    <div class="btn-wrapper">
    <button class="btn" @click="$emit('close')">Закрыть</button>
  </div>
  </div>.
</template>

<style scoped>
 .btn{
  margin: 0 auto;
  background-color: rgb(255, 255, 255);
  font-size: 14px;
  border: 1px solid ;   
  color: rgb(243, 142, 0);
  border-radius: 10px;
  width: 90px;
  height: 30px;
  cursor: pointer;
 }
 .btn:hover{
  color: rgb(255, 255, 255);
  background-color: rgb(255, 156, 17);
 }
 .btn-wrapper{
   align-items: center;
 }
 .ul{
  width: 200px;
 }
 .li{
  list-style-type: none;
 }

 .schedule-modal{
  position: absolute;
  color: aliceblue;
  background-color: rgb(255, 255, 255);
  transform: scaleY(-150px);
  border: 1px solid rgb(47, 216, 0);
  border-radius: 10px;
  max-width: 200px;
 }
</style>
