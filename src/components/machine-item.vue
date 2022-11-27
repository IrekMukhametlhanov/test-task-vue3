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
    <h2 class="machine_serial">{{ machineJoined.serialNumber }}</h2>
    <ul class="ul_tags">
      <li class="tags_li" key="tag" v-for="tag in machineJoined.type.tags">
        <p class="tags_name">{{ getTagName(tag) }}</p>
      </li>
    </ul>
  </div>
    <p class="location-address">адрес: {{ machineJoined.tradePoint.location.address }}</p>
    <p class="floor">Этаж: {{ machineJoined.floor }}</p>
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
    border: 1px solid lightgray;
    border-radius: 10px;
    margin-top: 5px;
  }
  .wrapper_items{
    display: flex;
    height: 37vh;
    flex-direction: column;
    margin: 10px 15px 10px 20px;
    flex: 2;
  }
  
  .top-wrapper{
    display: flex;
    align-items: center;
    text-align: center;
  }
  
  .machine_serial{
    width: 100px;
    height: 30px;
    padding-top: 3px;
    color: rgb(255, 255, 255);
    background-color: rgb(166, 4, 199);
    border: 1px solid rgb(166, 4, 199);
    border-radius: 5px;
    box-shadow: 2px 2px 2px 1px rgba(185, 183, 183, 0.2);
  }
  .ul_tags{
    display: flex;
    font-size: 15px;
  }
.image-map{
  left: 0;
  top: 0;
  max-width: 40vw;
  max-height: 37vh;
  margin-right: 5px;
}
.serial-number{
  color: rgb(149, 66, 66);
}

.tags_li{ 
  display: flex;
 align-items: center;
  list-style-type: none;
  margin-left: 3px;

}

.tags_name{
  display: flex;
  color: rgb(255, 255, 255);
  background-color: rgb(243, 142, 0);
  max-width: 180px;
  height: 20px;
  text-align: center;
  padding: 5px;
  font-size: 15px;
  font-weight: bolder;
  list-style-type: none;
  border: 1px solid rgb(243, 142, 0);
  margin-left: 2px;
  border-radius: 5px;
  box-shadow: 2px 2px 2px 1px rgba(10, 10, 10, 0.2);
  
}

.location-address{
  font-size: 15px;
  font-weight: bold;
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
  color: rgb(244, 66, 2);
  font-size: 20px;
  font-weight: bolder;

}
.trade-point{
  color: tomato;
}
</style>
