<template>
  <div class="home">
    <h1>Lista de Juegos Disponibles</h1>
    <div class="games">
      <GameCard
        v-for="game in games" :key="game.id" :id="game.id" :src="game.background_image" :name="game.name" :rating="game.rating" :release="game.released" :update="game.updated">
      </GameCard>
    </div>
    
  </div>
</template>

<script>
// @ is an alias to /src
import GameCard from '@/components/GameCard.vue';
export default {
  name: 'HomeView',
  // props: {},
  data: function(){
    return {
      games:[],
    }
  },
  // computed: {},
  methods: {
    async fetchGames(){
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
        this.games = json.results
        console.log(this.games[0])

      }
      catch(error){
            console.log("Error fetch", error)
      }
    }
  },
  // watch: {},
  components: {
    GameCard
  },
  // mixins: [],
  // filters: {},
  // -- Lifecycle Methods
  created(){
    this.fetchGames()
  }
  // -- End Lifecycle Methods
}
</script>

<style scoped>
  h1{
    margin-top: 1.25rem;
    margin-left: 15rem;
    color: rgb(53, 53, 53);
  }
  .games{
    width: 80%;
    margin: 0 auto;
    margin-top: 30px;
    display: flex;
    flex-wrap: wrap;
    justify-content: space-around;
    row-gap: 20px;
  }
</style>