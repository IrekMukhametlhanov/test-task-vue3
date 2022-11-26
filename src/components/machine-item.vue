<script setup lang="ts">
import ScheduleModal from './schedule-modal.vue';
import { ref } from 'vue';
import { getStaticMapImage } from '../services/maps.service';
import { useStore } from '../store';
import { getTagName } from '../utils/get-tage-names';
type Props = {
  id: number;
};
const props = defineProps<Props>();
const store = useStore();
const machineJoined = store.getters.machineJoined(props.id);
const mapImage = getStaticMapImage({
  lat: machineJoined.tradePoint.location.latitude,
  lng: machineJoined.tradePoint.location.longitude,
});
const scheduleModalOpen = ref<boolean>(false);
</script>

<template>
  <div class="main_wrapper">
  <div class="wrapper_items">
    <div class="top-wrapper">
    <h2>{{ machineJoined.serialNumber }}</h2>
    <ul class="ul-tags">
      <li class="tags-li" key="tag" v-for="tag in machineJoined.type.tags">
        <p class="tags-li">{{ getTagName(tag) }}</p>
      </li>
    </ul>
  </div>
    <p class="location-address">{{ machineJoined.tradePoint.location.address }}</p>
    <p>Этаж: {{ machineJoined.floor }}</p>
    <button class="btn_schedule" @click="scheduleModalOpen = true">Время работы</button>
    <div v-if="scheduleModalOpen">
      <ScheduleModal
      :schedule="machineJoined.tradePoint.workingTime"
      @close="scheduleModalOpen = false"
      />
    </div>
  </div>
 <div class="image-map"> 
  <img  class="image-map" :src="mapImage" />
 </div>
</div>
</template>
<style scoped>
  .main_wrapper{
    display: flex;
    align-items: center;
  }
  .wrapper_items{
    display: flex;
    height: 37vh;
    border: 2px solid lightgray;
    border-radius: 13px;
    flex-direction: column;
    background-color: rgb(255, 255, 255);
    margin: 5px;
    border: 2px solid lightgray;
    flex: 2;
  }
  
  .top-wrapper{
    display: flex;
  }

  .ul-tags{
    display: flex;
    font-size: 15px;
  }
.image-map{
  left: 0;
  top: 0;
  max-width: 40vw;
  max-height: 37vh;
}
.serial-number{
  color: red;
}

.tags-li{ 
  display: flex;
  color: rgb(32, 213, 0);
  width: 100px;
  height: 50px;
  text-align: center;
  align-items: center;
  font-size: 20px;
  font-weight: bolder;
  list-style-type: none;
  border: 1px solid black;
  border-radius: 10px;
}

.location-address{
  color: blue;
}
.btn_schedule {
  background-color: rgb(255, 255, 255);
  font-size: 14px;
  border: 1px solid ;
  color: rgb(243, 142, 0);
  border-radius: 15px;
  width: 140px;
  height: 50px;
  cursor: pointer;
}

.btn_schedule:hover{
  color: rgb(255, 255, 255);
  background-color: rgb(255, 156, 17);
}

.floor{
  color: rgb(0, 228, 125);
  font-weight: bold;

}
.trade-point{
  color: tomato;
}
</style>
