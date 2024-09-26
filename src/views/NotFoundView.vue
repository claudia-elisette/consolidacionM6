<template>
    <div>
        <h1>404</h1>
        <h2>Not Found</h2>
    </div>
</template>

<script>
export default {
    name: 'NotFoundView',
    // props: {},
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
    div{
        width: 60%;
        max-width: 700px;
        height: 50vh;
        margin: 0 auto;
        margin-top: 100px;
        background: linear-gradient(315.85deg, #8a62dd 0%, #309999 100%), radial-gradient(circle farthest-side at 50% 50%, #e88eff 0%, #6363e8 100%); background-blend-mode: lighten, normal;  background-position: 0 0, 0% 0%;
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        color: white;
    }
    h1{
        font-size: 10rem;
    }
</style>