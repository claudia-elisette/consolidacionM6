<template>
    <div>
        <h1>Escribe tu opinión para el juego: {{ game.name }}</h1>
        <div class="container">
            <OpinionCard :name="game.name" :src="game.background_image" :rating="game.rating"></OpinionCard>
            <form action="">
                <label for="">Nombre</label>
                <input type="text" required>
                <label for="">Opinion</label>
                <textarea name="" id="" placeholder="Tu opinión aquí..." required></textarea>
                <input type="submit">
            </form>
        </div>
        

        
    </div>
    
</template>

<script>
import OpinionCard from '@/components/OpinionCard.vue';
export default {
    name: 'OpinionView',
    props: {
        id:{
            type:Number,
            Required:true,
        },
    
    },
    data: function(){
        return {
            game:{
                id:this.id,
                name:"",
                background_image:"",
                rating:""
            },
            opiniones:[],
            
        }
    },
    // computed: {},
    methods: {
        async fetchGame(id){
            try{
                const response = await fetch("https://api.rawg.io/api/games?key=422b50c173204f95b53cf23cdc00f065")
                
                if(!response.ok){
                        if(response.status === 404){
                            alert("Juegos no disponibles")
                            return
                        }else{
                            throw new Error("HTTP error" + response.status)
                        }
                }

                const json = await response.json()
                const data = json.results

                this.game = data.find(game=> game.id == id)
                console.log(this.game)

            }
            catch(error){
                    console.log("Error fetch", error)
            }
    }
    },
    // watch: {},
    components: {
        OpinionCard
    },
    // mixins: [],
    // filters: {},
    // -- Lifecycle Methods
    created(){
        this.fetchGame(this.game.id)
    }
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
    .container{
        width: 60%;
        display: grid;
        grid-template-columns: max-content max-content;
        justify-content: space-between;
        margin: 50px auto;
    }
    form{
        align-self: center;
        display: grid;
        grid-template-columns: 30rem;
        grid-template-rows: 2rem 3rem 2rem 4rem 4rem;
        justify-content: space-between;

    }
    input, textarea{
        margin-bottom: 20px;
    }
</style>