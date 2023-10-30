<template>
<div>
    <h2>{{ foodName }}
        <img src="/img_quality.svg" v-show="isFavorite">
    </h2>
    <p>{{ foodDesc }}</p>
    <!-- <p>{{ foodIsFavorite }}</p> -->
    <!-- @ is shorthand v-on -->
    <button @:click="toogleFavorite">Favorite</button>
    <!-- <p id="red">You have clicked me {{ clicks }} times.</p> -->
</div>
</template>

<script>
export default{
    //you can specify which element gets the fallthrough attributes we can mark the element using $attrs
    // <li v-bind="$attrs">{{ itemName }}</li>
    //id red connects to the style #red
    //use props to pass data to components via custom attributes
    //use camelCase for props names
    // when a component is created in the parent element it cannot be change 
    // the value of the prop recived in the child element, so we cant change the props(read-only)
    // so we have to create a new data value foodIsFavorite and set it to the prop isFavorite, do all computation to foodIsFavorite
    //but use the props in the template 
    // $emit() to create custom event in the child component that can be captured in the parent
    // emit is used to poass inofrmation from the child compent to the parent 
    data() {
        return{
            name : 'apples',
            message: 'I like apples',
            foodIsFavorite: this.isFavorite,
        }
    },
    props:{
        //you should define props types
        foodName: {
            type: String, 
            //and add required for all required props, shows warning in console
            required: true
        },
        foodDesc: {
            type: String,
            required: false,
            //add default string value
            default:'Default string',
            validator: function(value){
                if(value.length > 20 && value.length < 50) {
                    return true
                } else {
                    return false
                }
            }
        },
        isFavorite: {
            type: Boolean, 
            required: false
        }
    },
    emits: ['toogle-favorite'],
    methods:{
        countClicks(){
            //make sure to use this.
            this.clicks++;
        }, 
        toogleFavorite() {
            // this.foodIsFavorite = !this.foodIsFavorite;
            //changing the favorite status in app instead because that is where it is stored first 
            //in a larger project the data might come from a database 
            //connected in App and we want a change happening from the component to make a change in the database, so we need to communicate back to the parent from the child component
            //use food name because it is unique for each food item
            this.$emit('toggle-Favorite',this.foodName);
        }
    }
}
</script>
<style>
  #red {
    font-weight: bold ;
    color: rgb(144, 12, 12);
  }
  img {
    height: 1.5em;
    float: right;
  }
</style>
