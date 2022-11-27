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
  <div class="schedule">
    <p class="time">Время работы</p>
    <ul class="ul">
      <li class="li" :key="day" v-for="(value, day) in schedule">
        {{ day }}: {{ value }}
      </li>
    </ul>
    <div class="btn-wrapper">
    </div>
  </div>
  <div class="btn-wrapper">
  <button class="btn" @click="$emit('close')">Закрыть</button>
  </div>
</div>
</template>

<style scoped>


.ul{
  width: 200px;
}
.li{
  list-style-type: none;
  color: rgb(255, 255, 255);
}

 .time{
  text-align: center;
}

 .schedule-modal{
   position: relative;
   font-weight: bold;
   color: rgb(255, 255, 255);
  background-color: rgba(0, 9, 180, 0.801);
  transform: scaleY(+500px);
  border: 1px solid rgba(38, 32, 123, 0.4);
  border-radius: 8px;
  max-width: 200px;
 }

 .schedule{
  margin: 0 auto;
 }
  .btn-wrapper{
    text-align: center;
    padding: 5px;
  }
  .btn{
    margin: 0 auto;
    background-color: rgb(255, 255, 255);
    font-size: 14px;
    border: 1px solid ;   
    text-align: center;
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
</style>
