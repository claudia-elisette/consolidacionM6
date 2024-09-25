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
        border: 1px solid rgb(161, 158, 158);
        border-radius: 5px;
    }
    img{
        width: 100%;
        height: 18rem;
    }
    .card__data{
        height: 80px;
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: space-around;
    }
    h4{
        font-weight: 400;
    }
</style>