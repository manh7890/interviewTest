
  
  <script setup lang="ts">
  import { ref, defineProps, defineEmits } from 'vue'
  const emit =defineEmits(['next-tab','error'])
  
  const mealCategory=ref<string>("")
  const mealCategoryList:string[]=["","breakfast","lunch","dinner"]
  const numberValue=ref<number>(0)
  function clickNextEvent(numberValue:number ,mealCategory:string ) {
    console.log(numberValue,mealCategory)
    if (numberValue>0&& mealCategory.trim()!==""){
        emit('next-tab',numberValue,mealCategory)
    }else{
        emit('error', "vui lòng xem lại các trường đã chọn")
    }
    
}
  </script>
  <template>
   
    <v-card
    class="mx-auto mb-6"
    max-width="344"
    title="User Registration"
  >
        <v-container>
        <p>Please Select a meal</p><br/>
        <v-select
        v-model="mealCategory"
        label="Select"
        :items="mealCategoryList"
        :rules="[v => !!v ,v=>v!=''] "
        required
        ></v-select><br/>
        <p>Please Enter Number of people</p><br/>
        <v-text-field
            v-model="numberValue"
            hide-details
            single-line
            type="number"
            :rules="[v => !!v ,v=>v>0,v=>v<11] "
            required
            />
        </v-container>
      <v-btn class="mb-6 float-r mr-4" @click="clickNextEvent(numberValue,mealCategory)">
        next

        
      </v-btn>
   
</v-card>
  </template>
  <style>
  .formOne{
    display: flex;
  justify-content: center; 
  align-items: center;
  }
  .float-r{
    float: right;
  }
  .mr-4{
    margin-right: 4px;
  }
  .mb-6{
    margin-bottom: 6px;
  }

  </style>
  