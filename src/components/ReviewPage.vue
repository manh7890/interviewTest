<template>
    <div >
        
        <span class="inline-block">Meal:      </span><span class="inline-block">{{ props.reservationData.meal }}</span><br>
        <span class="inline-block">No of People:     </span><span class="inline-block">{{ props.reservationData.people }}</span><br>
        <span class="inline-block">Restaurant:   </span><span class="inline-block">{{ props.reservationData.restaurant }}</span><br>
        <v-textarea
      name="input-7-1"
      variant="filled"
      label="Dish Info"
      readonly
      auto-grow
      :model-value="textDishInfo"
    ></v-textarea>
    </div>
    <v-btn class="mb-6 float-r mr-4" >
        Submit

        
      </v-btn>
      <v-btn class="mb-6 float-l ml-4" @click="clickPreviousEvent()">
        Previous

        
      </v-btn>
</template>

<script setup lang="ts">
 import { ref, defineProps, defineEmits } from 'vue'
 const emit =defineEmits(['previous'])
 interface ServDishs{
  dishName:string;
  numberServ:number;
}
    const props =defineProps(['reservationData'])
    const dishsInfo=ref<ServDishs[]>(props.reservationData.servDishs)
    var textDishInfo=""
    dishsInfo.value.forEach((dish:ServDishs) => {
        textDishInfo+=dish.dishName +  '     -     '+dish.numberServ+'\n'
    });
    function clickPreviousEvent(){
    emit('previous',"step-3")
}
</script>

<style scoped>
.inline-block{
    display:inline-block
}
</style>