<template>
  <!-- you need a key attribute for list of items -->
  <!-- : is shorthand for v-bind -->
  <div id="app">
    <h1>Food</h1>
    <food-item
    v-for="x in foods"
    :key="x.name"
    :food-name="x.name"
    :food-desc="x.desc"
    :is-favorite="x.favorite"
    @toggle-favorite="receiveEmit"
    />
</div>
</template>


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
    // create list of foods in parent or wherever you want to show many instances of a component
    return {
      foods: [
          { name: 'Apples',
            desc: 'Apples are a type of fruit that grow on trees.',
            favorite: true },
          { name: 'Pizza',
            desc: 'Pizza has a bread base with tomato sauce, cheese, and toppings on top.',
            favorite: false },
          { name: 'Rice',
            desc: 'Rice is a type of grain that people like to eat.',
            favorite: false },
          { name: 'Fish',
            desc: 'Fish is an animal that lives in water.',
            favorite: true },
          { name: 'Cake',
            desc: 'Cake is something sweet that tastes good.',
            favorite: false }
        ]
    };
  },
  methods:{
        //this is how we receive the food item name in the parent
        receiveEmit(foodId){
          const foundFood = this.foods.find(
            food => food.name === foodId
          );
          foundFood.favorite = !foundFood.favorite;
          //find goes through the foods array and looks
          // for an object with the name euqal to the food item we clicked
          // and returns that object as foundFood, then foodFood.favorite to be the oppsite to what it was before 
        }
      }
}
</script>


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
