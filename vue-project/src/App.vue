
<script>
//import to use components
import FoodItem from './components/FoodItem.vue'
//export default allows main.js to catch data with 
//import App from './App.vue' so it can be mounted 
//to set props use kabob for the naming 
//to use a prop that is not a string we have to use a v-bind
export default {
  name: "app",
  components: {
    FoodItem, //add components, use them using the kebob name
    //also must have div with the id app
  },
  data(){
    return {
      message:'text'
    }
  }
}
</script>

<template>
  <div id="app">
  <h1>Food</h1>
  <food-item 
  food-name="Apples"
  food-desc="Apples are a type of fruit that grow on trees."
  v-bind:is-favorite="true"/>
  <food-item food-name="Pizza"
  food-desc="Pizza has a bread base with tomato sauce, cheese, and toppings on top."
  v-bind:is-favorite="false"/>
  <food-item food-name="Rice"
  food-desc="Rice is a type of grain that people like to eat."
  v-bind:is-favorite="false"/>
</div>
</template>

<style>
  #app{
    display: flex;
    flex-wrap: wrap;
  }
  #app > div {
    border: dashed black 1px;
    margin: 10px;
    padding: 10px;
    background-color: lightgreen;
  }
</style>
