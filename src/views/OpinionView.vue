<template>
    <div>
        <h1>Escribe tu opinión para el juego: {{ name }}</h1>
    </div>
    
</template>

<script>
export default {
    name: 'OpinionView',
    props: {
        name:{
            type:String,
            Required:true,
        }
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
    h1{
        width: max-content;
        margin: 0 auto;
        margin-top: 20px;
        font-weight:lighter;
    }
</style>