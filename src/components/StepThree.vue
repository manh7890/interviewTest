
  
  <script setup lang="ts">
  import { ref, defineProps, defineEmits } from 'vue'
  const emit =defineEmits(['next-tab','error','previous'])
  const listDishInfo=ref<string[]>([])
    const dishValue=ref<string>("")
  const numberServ=ref<number>(0)
    const props =defineProps(['dishsData','peopleWillBeServe'])
    var currentServDish=0
    
    const dishsData=ref<string[]>(props.dishsData).value
  function clickNextEvent( ) {
    console.log(props)
    console.log(currentServDish,"currentServDish")
    if(Number(props.peopleWillBeServe) > Number(currentServDish)){
        emit('error', "Số xuất ăn phải lớn hơn hoặc bằng số người ăn")
    }else{
        emit('next-tab',listDishInfo.value)
        
    }
    }
function clickAddEvent(){
    console.log(dishValue.value,numberServ.value)
    if (dishValue.value.trim() !=""&&numberServ.value>0){
        currentServDish+=numberServ.value
        listDishInfo.value.push(dishValue.value +"  -  " + numberServ.value)
    dishsData.forEach((dish:string,idx:number)=>{
        if (dish==dishValue.value){
            dishsData.splice(idx, 1);
        }
        
    })
    dishValue.value=""
        numberServ.value=0
    }else{
        if (dishValue.value.trim() !=""){
            emit('error', "vui lòng xem lại các trường đã chọn")
        }
    }
}
function clickPreviousEvent(){
    emit('previous',"step-2")
}
  </script>
  <template>
   
    <v-card
    class="mx-auto mb-6"
    max-width="344"
    title="User Registration"
  >
        <v-container>
        <p>Please Select a Dish</p><br/>
        <v-select
        v-model="dishValue"
        label="Select"
        :items="dishsData"
        :rules="[v => !!v || dishsData.length<1,v=>v!=''|| dishsData.length<1] "
        :required="dishsData.length>0"
        ></v-select><br/>
        <p>Please Enter Number of Serving</p><br/>
        
        <v-text-field
            v-model="numberServ"
            hide-details
            single-line
            type="number"
            :rules="[v => !!v || dishsData.length<1,v=>v>0 || dishsData.length<1] "
            :required="dishsData.length>0"
            />
            
            
      <v-space></v-space>
        </v-container>
        <div style="display: flex;
  justify-content: space-between; 
  align-items: center;">
    <v-btn class="mb-6 ml-4" @click="clickPreviousEvent()">
        Previous

        
      </v-btn>
      <v-btn class="mb-6 " @click="clickAddEvent()">
        add

        
      </v-btn>
      <v-btn class="mb-6 mr-4" @click="clickNextEvent()">
        Next

        
      </v-btn>
        </div>
        
      
   
</v-card>
  </template>
  <style>
  .formOne{
    display: flex;
  justify-content: center; 
  align-items: center;
  }
  .float-l{
    float:left;
  }
  .ml-4{
    margin-left: 4px;
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
  .mb-12{
    margin-bottom: 12px;
  }
  </style>
  