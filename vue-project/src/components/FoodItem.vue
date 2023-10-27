<template>
<div>
    <h2>{{ foodName }}
        <img src="../../public/img_quality.svg" v-show="foodIsFavorite">
    </h2>
    <p>{{ foodDesc }}</p>
    <!-- <p>{{ foodIsFavorite }}</p> -->
    <button v-on:click="toogleFavorite">Favorite</button>
    <!-- <p id="red">You have clicked me {{ clicks }} times.</p> -->
</div>
</template>

<script>
export default{
    //id red connects to the style #red
    //use props to pass data to components via custom attributes
    //use camelCase for props names
    // when a component is created in the parent element it cannot be change 
    // the value of the prop recived in the child element, so we cant change the props(read-only)
    // so we have to create a new data value foodIsFavorite and set it to the prop isFavorite, do all computation to foodIsFavorite
    //but use the props in the template 
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
    methods:{
        countClicks(){
            //make sure to use this.
            this.clicks++;
        }, 
        toogleFavorite() {
            this.foodIsFavorite = !this.foodIsFavorite;
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
