<template>
  <div class="mainContainer">
    <div class="foodPicker">
      <v-alert :text="errMess" color="error"
  v-model="isAller"></v-alert>
      <v-card>
    <v-tabs
      v-model="tab"
      bg-color="primary"
    >
      <v-tab value="step-1">Item One</v-tab>
      <v-tab value="step-2" :disabled="currentAvailableTab<2">Item Two</v-tab>
      <v-tab value="step-3" :disabled="currentAvailableTab<3">Item Three</v-tab>
      <v-tab value="review" :disabled="currentAvailableTab<4">Review</v-tab>
    </v-tabs>
    <v-card-text>
      <v-window v-model="tab">
        <v-window-item value="step-1">
          <component :is="StepOne" :v-show="tab=='step-1'" v-on:next-tab="stepOneNextTab" v-on:error="errorHandle" />
        </v-window-item>

        <v-window-item value="step-2">
          <component :is="StepTwo" :v-show="tab=='step-2'" v-on:next-tab="stepTwoNextTab" v-on:error="errorHandle" v-on:previous="clickPreviousEvent" :restaurentData="restaurentData"/>
        </v-window-item>

        <v-window-item value="step-3">
          <component :is="StepThree" :v-show="tab=='step-3'" v-on:next-tab="stepThreeNextTab" v-on:previous="clickPreviousEvent" v-on:error="errorHandle" :dishsData="dishNameAvailable" :peopleWillBeServe="reservationData.people"/>
        </v-window-item>
        <v-window-item value="review">
          <component :is="ReviewPage" :v-show="tab=='review'" v-on:next-tab="stepThreeNextTab" v-on:previous="clickPreviousEvent" v-on:error="errorHandle" :reservationData="reservationData" />
        </v-window-item>
      </v-window>
    </v-card-text>
  </v-card>
      
    </div>
  </div>
   
</template>

<script setup lang="ts">
import { ref } from 'vue'
import  StepOne from './components/StepOne.vue'
import  StepTwo from './components/StepTwo.vue'
import  StepThree from './components/StepThree.vue'
import  ReviewPage from './components/ReviewPage.vue'


console.log(StepOne)
var tab=ref<string>("step-1")
interface Dish{
  id:number;
  name:string;
  restaurant:string;
  availableMeals:string[];
}
interface ServDishs{
  dishName:string;
  numberServ:number;
}
interface Reservation{
  meal:string;
  people:number;
  restaurant:string;
  servDishs:ServDishs[];
}
var reservationData:Reservation={
  meal:"",
  people:0,
  restaurant:"",
  servDishs:[]
}
var errMess=ref<string>("")
var isAller=ref<boolean>(false)
var currentAvailableTab=1
const  dishesData ={
  "dishes": [
    {
      "id": 1,
      "name": "Chicken Burger",
      "restaurant": "Mc Donalds",
      "availableMeals": ["lunch", "dinner"]
    },
    {
      "id": 2,
      "name": "Ham Burger",
      "restaurant": "Mc Donalds",
      "availableMeals": ["lunch", "dinner"]
    },
    {
      "id": 3,
      "name": "Cheese Burger",
      "restaurant": "Mc Donalds",
      "availableMeals": ["lunch", "dinner"]
    },
    {
      "id": 4,
      "name": "Fries",
      "restaurant": "Mc Donalds",
      "availableMeals": ["lunch", "dinner"]
    },
    {
      "id": 5,
      "name": "Egg Muffin",
      "restaurant": "Mc Donalds",
      "availableMeals": ["breakfast"]
    },
    {
      "id": 6,
      "name": "Burrito",
      "restaurant": "Taco Bell",
      "availableMeals": ["lunch", "dinner"]
    },
    {
      "id": 7,
      "name": "Tacos",
      "restaurant": "Taco Bell",
      "availableMeals": ["lunch", "dinner"]
    },
    {
      "id": 8,
      "name": "Quesadilla",
      "restaurant": "Taco Bell",
      "availableMeals": ["lunch", "dinner"]
    },
    {
      "id": 9,
      "name": "Steak",
      "restaurant": "BBQ Hut",
      "availableMeals": ["dinner"]
    },
    {
      "id": 10,
      "name": "Yakitori",
      "restaurant": "BBQ Hut",
      "availableMeals": ["dinner"]
    },
    {
      "id": 11,
      "name": "Nankotsu",
      "restaurant": "BBQ Hut",
      "availableMeals": ["dinner"]
    },
    {
      "id": 12,
      "name": "Piman",
      "restaurant": "BBQ Hut",
      "availableMeals": ["dinner"]
    },
    {
      "id": 13,
      "name": "Vegan Bento",
      "restaurant": "Vege Deli",
      "availableMeals": ["lunch"]
    },
    {
      "id": 14,
      "name": "Coleslaw Sandwich",
      "restaurant": "Vege Deli",
      "availableMeals": ["breakfast"]
    },
    {
      "id": 15,
      "name": "Grilled Sandwich",
      "restaurant": "Vege Deli",
      "availableMeals": ["breakfast"]
    },
    {
      "id": 16,
      "name": "Veg. Salad",
      "restaurant": "Vege Deli",
      "availableMeals": ["lunch", "dinner"]
    },
    {
      "id": 17,
      "name": "Fruit Salad",
      "restaurant": "Vege Deli",
      "availableMeals": ["lunch", "dinner"]
    },
    {
      "id": 18,
      "name": "Corn Soup",
      "restaurant": "Vege Deli",
      "availableMeals": ["lunch", "dinner"]
    },
    {
      "id": 19,
      "name": "Tomato Soup",
      "restaurant": "Vege Deli",
      "availableMeals": ["lunch", "dinner"]
    },
    {
      "id": 20,
      "name": "Minestrone Soup",
      "restaurant": "Vege Deli",
      "availableMeals": ["lunch", "dinner"]
    },
    {
      "id": 21,
      "name": "Pepperoni Pizza",
      "restaurant": "Pizzeria",
      "availableMeals": ["lunch", "dinner"]
    },
    {
      "id": 22,
      "name": "Pepperoni Pizza",
      "restaurant": "Pizzeria",
      "availableMeals": ["lunch", "dinner"]
    },
    {
      "id": 23,
      "name": "Hawaiian Pizza",
      "restaurant": "Pizzeria",
      "availableMeals": ["lunch", "dinner"]
    },
    {
      "id": 24,
      "name": "Seafood Pizza",
      "restaurant": "Pizzeria",
      "availableMeals": ["lunch", "dinner"]
    },
    {
      "id": 25,
      "name": "Deep Dish Pizza",
      "restaurant": "Pizzeria",
      "availableMeals": ["dinner"]
    },
    {
      "id": 26,
      "name": "Chow Mein",
      "restaurant": "Panda Express",
      "availableMeals": ["lunch", "dinner"]
    },
    {
      "id": 27,
      "name": "Mapo Tofu",
      "restaurant": "Panda Express",
      "availableMeals": ["lunch", "dinner"]
    },
    {
      "id": 28,
      "name": "Kung Pao",
      "restaurant": "Panda Express",
      "availableMeals": ["lunch", "dinner"]
    },
    {
      "id": 29,
      "name": "Wontons",
      "restaurant": "Panda Express",
      "availableMeals": ["lunch", "dinner"]
    },
    {
      "id": 30,
      "name": "Garlic Bread",
      "restaurant": "Olive Garden",
      "availableMeals": ["breakfast", "lunch", "dinner"]
    },
    {
      "id": 31,
      "name": "Ravioli",
      "restaurant": "Olive Garden",
      "availableMeals": ["lunch", "dinner"]
    },
    {
      "id": 32,
      "name": "Rigatoni Spaghetti",
      "restaurant": "Olive Garden",
      "availableMeals": ["lunch", "dinner"]
    },
    {
      "id": 33,
      "name": "Fettucine Pasta",
      "restaurant": "Olive Garden",
      "availableMeals": ["lunch", "dinner"]
    }
  ] as Dish[]
}
var restaurentData:string[]=[]
function stepOneNextTab(numberPeople:number,mealCategory:string) {
  
  tab.value="step-2"
  reservationData.meal=mealCategory
  reservationData.people=numberPeople
  currentAvailableTab=2

  dishesData.dishes.forEach((vl)=>{
    if(vl.availableMeals.includes(reservationData.meal)){
      if(!restaurentData.includes(vl.restaurant))
      restaurentData.push(vl.restaurant)
    }
  })
}
var dishNameAvailable:string[]=[]
function stepTwoNextTab(restaurant:string){
  reservationData.restaurant = restaurant
  tab.value="step-3"
  currentAvailableTab=3
  
  dishesData.dishes.forEach((vl)=>{
    if(vl.availableMeals.includes(reservationData.meal)&&vl.restaurant==restaurant){
      if(!dishNameAvailable.includes(vl.name))
      dishNameAvailable.push(vl.name)
    }
  })
}
function stepThreeNextTab(listDishInfo:string[]){
  listDishInfo.forEach((dishinfo:string)=>{
    let dishInfo=dishinfo.split("-");
    tab.value="review"
  currentAvailableTab=4
    reservationData.servDishs.push({
      dishName:dishInfo[0],
      numberServ:Number(dishInfo[1])
    })
  })
}
function clickPreviousEvent(previouslyStep:string){
  tab.value=previouslyStep
}
function errorHandle(errorMessage:string){
  errMess.value=errorMessage
 isAller.value=true
 setTimeout(()=>{isAller.value=false},1000)
}

</script>

<style>
.foodPicker{
  
  background-color: white;
}
.mainContainer{
  display: flex;
  justify-content: center; 
  align-items: center;
  height: 100vh;
  width: 100vw;
  background-image: url("./assets/images.jpeg");
  background-repeat: no-repeat;
  background-size: 100vw 100vh;
}
.v-card{
  min-height: 55vh;
}
.v-alert {
  position: fixed !important;
  left: 50%;
  margin: 0 auto;  
  right: 2px;
  top:8px;
}
</style>
