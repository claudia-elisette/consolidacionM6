<template>
    <div class="card">
        <div class="card__img">
            <img :src="src" alt="GameImg">
        </div>
        <div class="card__data">
            <h3 class="card__item card__item-b">{{ name }}</h3>
            <h4 class="card__item">Rating: {{ rating }}</h4>
            <h4 class="card__item">Released: {{ release }}</h4>
            <h4 class="card__item">Updated: {{ update }}</h4>
            <div class="card__click card__item-b">
                <button @click="redirectTo(id)">Opinar</button>
                <a href="#"><i class="fa-solid fa-heart"></i></a>
            </div>
        </div> 
        
    </div>
</template>

<script>
export default {
    name: 'game-comp',
    props: {
        id:{
            type:Number,
            Required:true
        },
        src:{
            type:String,
            Required:true
        },
        name:{
            type:String,
            Required:true
        },
        rating:{
            type:Number,
            Required:true
        },
        release:{
            type:String,
            Required:true
        },
        update:{
            type:String,
            Required:true
        },
    },
    data: function(){
        return {}
    },
    // computed: {},
    methods: {
        redirectTo(id){
            this.$router.push("/opiniones/"+id)
        }
    }
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
        display: flex;
        flex-direction: column;
        justify-content: space-between;
        border: 1px solid rgb(202, 202, 202);
        border-radius: 5px;
        width: 25rem;
    }
    img{
        width: 100%;
        height: 200px;
    }
    .card__data{
        display: grid;
        grid-template-rows: max-content max-content max-content max-content max-content
    }
    .card__item{
        border-bottom: 1px solid rgb(202, 202, 202);
        padding: 5px;
        padding-left: 10px;
    }
    .card__item-b{
        padding: 10px;
    }
    button{
        border: none;
        padding: 10px 20px;
        border-radius: 5px;
        background-color: rgb(31, 117, 247);
        color: #fff;
        margin-right: 10px;
        cursor: pointer;
    }
    i{
        color: red;
    }
</style>