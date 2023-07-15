<template>
    <div class="home">
        <div class="col-md-12">
            <div class="row m-5">
                <div class="col-lg-2 mb-3 d-flex align-items-stretch" v-for="(game, index) in games" :key="index">
                    <div class="card bg-black" style="width: 18rem;">
                        <img :src="game.background_image" class="card-img-top" alt="Imagen de fondo">
                        <div class="card-body">
                            <h5 class="card-title text-light">{{ game.name }}</h5>
                            <p class="card-text text-center text-light">Released date: {{ game.released }}</p>
                            <a href="#" class="btn btn-light" @click="gameDetail(game.id)">Give us your opinion</a>
                            <a href="#" class="mx-3" @click="adminPage(game.id)"><svg xmlns="http://www.w3.org/2000/svg" class="icon icon-tabler icon-tabler-heart" width="36" height="36" viewBox="0 0 24 24" stroke-width="1.5" stroke="#f43d45" fill="#f43d45" stroke-linecap="round" stroke-linejoin="round">
                              <path stroke="none" d="M0 0h24v24H0z" fill="none"/>
                              <path d="M19.5 12.572l-7.5 7.428l-7.5 -7.428a5 5 0 1 1 7.5 -6.566a5 5 0 1 1 7.5 6.572" />
                              </svg>
                            </a>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
// @ is an alias to /src
// import HelloWorld from '@/components/HelloWorld.vue'
import axios from 'axios'

export default {
    name: "HomeView",
    data() {
        return {
            games: [],
        };
    },
    methods: {
        axiosGames() {
            axios.get(`https://api.rawg.io/api/games?key=7e07fb9277eb4621be4e3e3f6f69213c`)
                .then((response) => {
                // handle success
                console.log(response.data.results);
                this.games = response.data.results;
            })
                .catch(function (error) {
                // handle error
                console.log(error);
            });
        },
        gameDetail(id) {
            this.$router.push(`/opinion/${id}`);
        },
        adminPage(id) {
            this.$router.push(`/admin/${id}`);
        }
    },
    created() {
        this.axiosGames();
    }
}
</script>

<style scoped>
.card-img-top {
    width: 100%;
    height: 10vw;
    object-fit: cover;
}
.card-title {
  white-space: nowrap; 
  overflow: hidden; 
  text-overflow: ellipsis; 
}
</style>