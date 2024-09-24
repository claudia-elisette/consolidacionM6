<template>
    <div class="card">
        <div class="card__img">
            <img :src="src" alt="GameImg">
        </div>
        <div class="card__data">
            <h3 class="card__item">{{ name }}</h3>
            <h4 class="card__item">Rating: {{ rating }}</h4>
        </div> 
    </div>
</template>

<script>
export default {
    name: 'opinionCard-comp',
    props: {
        name:{
            type:String,
            required:true,
        },
        src:{
            type:String,
            required:true,
        },
        rating:{
            type:Number,
            required:true,
        },
    },
    data: function(){
        return {}
    },
    // computed: {},
    //methods: {}
    // watch: {},
    // components: {},
    // mixins: [],
    // filters: {},
    // -- Lifecycle Methods
    // -- End Lifecycle Methods
}
</script>

<style scoped>
    .card{
        width: 25rem;
    }
    img{
        width: 100%;
        height: 18rem;
    }
    .card__data{
        display: flex;
        flex-direction: column;
        align-items: center;
    }
</style>