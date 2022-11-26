<script setup lang="ts">
import ScheduleModal from './schedule-modal.vue';
import type { ITradePoint } from '../interfaces/trade-point.interface';
import type { IMachine } from '../interfaces/machine.interface';
import type { IMachineType } from '../interfaces/machine-type.interface';
import { onBeforeMount, ref } from 'vue-demi';
import { getStaticMapImage } from '../services/maps.service';
import { getTradePoint } from '../services/trade-points.service';
import { getMachineType } from '../services/machines.service';

type Props = {
  machine: IMachine;
};

const props = defineProps<Props>();

const tradePoint = ref<ITradePoint>();
const machineType = ref<IMachineType>();
const mapImage = ref<string>();

const scheduleModalOpen = ref<boolean>(false);

onBeforeMount(async () => {
  const tradePointId = props.machine.tradePointId;

  tradePoint.value = await getTradePoint(tradePointId);

  const machineTypeId = props.machine.typeId;

  machineType.value = await getMachineType(machineTypeId);

  mapImage.value = getStaticMapImage({
    lat: tradePoint.value.location.latitude,
    lng: tradePoint.value.location.longitude,
  });
});
</script>

<template>
  <div class="main_wrapper">
  <div class="wrapper_items">
<div class="top-wrapper">
    <h2 class="serial-number">{{ machine.serialNumber }}</h2>
    <ul class="ul-tags" v-if="machineType">
      <li class="tags-li" :key="tag" v-for="tag in machineType.tags">
        <p class="tags">{{ tag }}</p>
      </li>
    </ul>
  </div>
    <p class="location-address">{{ tradePoint && tradePoint.location.address }}</p>

    
    <p class="floor">Этаж: {{ machine.floor }}</p>

    <button class="btn_schedule" 
    @click="() => {
        scheduleModalOpen = true;
      }
    ">
      Schedule
    </button>
    <div class="trade-point" v-if="tradePoint && scheduleModalOpen">
      <ScheduleModal :schedule="tradePoint.workingTime" @close="
        () => {
          scheduleModalOpen = false;
        }
      " />
    </div>
  </div>
 <div class="image-wrapper">
  <img :src="mapImage" class="image-map" />
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
    flex-direction: column;
    background-color: aliceblue;
    margin: 5px;
    border: 2px solid lightgray;
    flex: 2;
  }
  
  .top-wrapper{
    display: flex;
  }

  .ul-tags{
    font-size: 15px;
  }

  li{
    text-decoration: none;
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

.tags{
  color: violet;
}
.tags-li{
  color: yellowgreen;
  list-style-type: none;
}

.location-address{
  color: blue;
}
.btn_schedule {
  background-color: rgb(211, 211, 211);
  border-radius: 15px;
  width: 100px;
  height: 50px;
}

.btn_schedule :hover{
  background-color: aqua;
}

.floor{
  color: rgb(0, 0, 0);
  font-weight: bold;

}
.trade-point{
  color: tomato;
}
</style>
