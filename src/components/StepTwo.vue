<template>
     <v-card
    class="mx-auto mb-6"
    max-width="344"
    title="User Registration"
  >
        <v-container>
        <p>Please Select a Restaurant</p><br/>
        <v-select
        v-model="restaurant"
        label="Select"
        :items="props.restaurentData"
        :rules="[v => !!v ,v=>v!=''] "
        required
        ></v-select><br/>
        
        </v-container>
        
      <v-btn class="mb-6 float-r mr-4" @click="clickNextEvent(restaurant)">
        Next

        
      </v-btn>
      <v-btn class="mb-6 float-l ml-4" @click="clickPreviousEvent()">
        Previous

        
      </v-btn>
   
</v-card>
</template>

<script setup lang="ts">
import { ref, defineProps, defineEmits } from 'vue'
const props =defineProps(['restaurentData'])
const emit =defineEmits(['next-tab','error','previous'])
    console.log(props.restaurentData)
  const restaurant=ref<string>("")
  const mealCategoryList:string[]=["","breakfast","lunch","dinner"]
  function clickNextEvent(restaurant:string ) {
    console.log(restaurant)
    if (restaurant!==""){
        emit('next-tab',restaurant)
    }else{
        emit('error', "vui lòng xem lại các trường đã chọn")
    }
    
}
function clickPreviousEvent(){
    emit('previous',"step-1")
}
</script>

<style scoped>

</style>