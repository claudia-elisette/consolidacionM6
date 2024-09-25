<template>
    <div>
        <h1>Escribe tu opinión para el juego: {{ game.name }}</h1>
        <div class="container">
            <OpinionCard :name="game.name" :src="game.background_image" :rating="game.rating"></OpinionCard>
            <form v-if="!edit">
                <label for="">Nombre</label>
                <input type="text" v-model="opinionName" required>
                <label for="">Opinion</label>
                <textarea v-model="opinionText" placeholder="Tu opinión aquí..." required></textarea>
                <input class="submit" type="submit" value="Agregar" @click.prevent="pushOpinion">
            </form>
            <form v-if="edit">
                <label for="">Nombre</label>
                <input type="text" v-model="opinionName" required>
                <label for="">Opinion</label>
                <textarea v-model="opinionText" placeholder="Tu opinión aquí..." required></textarea>
                <input class="submit" type="submit" value="Actualizar" @click.prevent="updateOpinion(opinionId)">
            </form>
        </div>
        <h1>A continuación podrás ver tu opinión</h1>
        <div class="noOpinion" v-if="opiniones.length == 0">
            <p>No existen opiniones para mostrar</p>
        </div>
        <div class="opinion" v-for="opinion in opiniones" :key="opinion.id">   
            <div class="opinionHeader">
                <p>Opinión creada por: <strong>{{ opinion.name }}</strong></p>
            </div>
            <div class="opinionText">
                <p><strong>Opinion:</strong> {{ opinion.opinion }}</p>
            </div>
            <div class="opinionBtn">
                <button class="deleteBtn" @click="deleteOpinion(opinion.id)">Eliminar</button>
                <button class="editBtn" @click="editOpinion(opinion.id)">Editar</button>
            </div>
        </div>

        
    </div>
    
</template>

<script>
import OpinionCard from '@/components/OpinionCard.vue';
export default {
    name: 'OpinionView',
    props: {
        id:{
            type:String,
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
            opinionName:"",
            opinionText:"",
            opinionId:"",
            edit:false
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

            }
            catch(error){
                    console.log("Error fetch", error)
            }
        },
        pushOpinion(){
            let opinion = {
                id:Math.floor(Math.random()*1000),
                name:this.opinionName,
                opinion:this.opinionText
            }
            this.opiniones.push(opinion)
            this.opinionName = ""
            this.opinionText = ""
        },
        deleteOpinion(id){
            let index = this.opiniones.findIndex((opinion)=> opinion.id == id)
            this.opiniones.splice(index,1)
        },
        editOpinion(id){
            this.edit = true
            let index = this.opiniones.findIndex((opinion)=> opinion.id == id)
            this.opinionId = this.opiniones[index].id
            this.opinionName = this.opiniones[index].name
            this.opinionText = this.opiniones[index].opinion
            
        },
        updateOpinion(id){
            this.edit = false
            let index = this.opiniones.findIndex((opinion)=> opinion.id == id)
            this.opiniones[index].name = this.opinionName
            this.opiniones[index].opinion = this.opinionText
            this.opinionName = ""
            this.opinionText = ""
        },

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
        display: flex;
        flex-wrap: wrap;
        row-gap: 1.875rem;
        column-gap: 10%;
        justify-content: center;
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
        margin-bottom: 1.25rem;
    }
    .submit{
        border: none;
        background-color: rgb(61, 184, 255);
        border-radius: 5px;
    }
    .noOpinion{
        background-color: rgb(235, 123, 123);
        margin-top: 1.25rem;
        padding: 1.25rem;
    }
    .opinion{
        margin: 0 auto;
        margin-top: 20px;
        width: 80%;
        border: 1px solid rgb(182, 182, 182);
        border-radius: 5px;
    }
    .opinionHeader{
        background-color: rgba(169, 201, 228, 0.541);
        padding: 1.25rem;
        color: rgb(19, 132, 207);
        border-bottom: 1px solid rgb(182, 182, 182);

    }
    .opinionText{
        padding: 1.25rem;
        padding-bottom: 0.5rem;
    }
    .opinionBtn{
        padding: 0.5rem;
    }
    button{
        border: none;
        width: 100px;
        height: 40px;
        margin-right: 20px;
        border-radius: 5px;
    }
    .editBtn{
        background-color: rgb(240, 201, 28);
    }
    .deleteBtn{
        background-color: rgb(202, 20, 20);
        color:white;
    }
</style>