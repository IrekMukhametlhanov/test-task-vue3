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
    <p>Время работы</p>
    <ul>
      <li class="li" :key="day" v-for="(value, day) in schedule">
        {{ day }}: {{ value }}
      </li>
    </ul>

    <button class="btn" @click="$emit('close')">Закрыть</button>
  </div>
</template>

<style scoped>
 .btn{
  text-align: center;
  width: 80px;
  height: 30px;
  border-radius: 8px;
 }

 .li{
  list-style-type: none;
 }
</style>
