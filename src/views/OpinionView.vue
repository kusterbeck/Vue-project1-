<template>
    <div class="container">
        <h1 class="my-4">Escribe tu opinion para el juego: {{ game.name }}</h1>
        <form class="form-control" action="" id="formulario">
            <label class="row m-2" for="name">Nombre</label>
            <input class="row col-12 m-2" type="text" placeholder="Tu Nombre" v-model="name" id="name">
            <label class="row m-2" for="comentario">Comentario</label>
            <input class="row col-12 m-2" type="text" placeholder="Tu opinión debe ir aquí" v-model="comentario" id="comentario">    
            <button v-if="!isEditOn" class="btn btn-info d-flex flex-start m-2" @click="getPersonalData()" button type="button">Agregar</button>
            <button v-else class="btn btn-info d-flex flex-start m-2" @click="updateOpinion()">Actualizar</button>
        </form>
        <h1 class="my-4">A continuación podrás ver tu opinión</h1>
        <p v-if="opinions === ''" class="bg-danger bg-opacity-50 p-3">No existen opiniones para mostrar.</p>
        <div v-else>
            <div class="accordion" id="accordionExample">
                <template v-for="(opinion, index) in opinions" >
                    <div class="accordion-item" :key="index">
                        <h2 class="accordion-header" id="headingOne">
                            <button class="accordion-button" type="button" data-bs-toggle="collapse" data-bs-target="#collapseOne" aria-expanded="true" aria-controls="collapseOne">
                                Opinion creada por: {{ opinion.name }}
                            </button>
                        </h2>
                        <div id="collapseOne" class="accordion-collapse collapse show" aria-labelledby="headingOne" data-bs-parent="#accordionExample">
                            <div class="accordion-body">
                                {{ opinion.comentario }}
                            </div>
                            <div class="d-flex flex-start">
                                <button class="btn btn-danger m-3" type="button" @click="deleteOpinion(index)">Eliminar</button>
                                <button class="btn btn-warning m-3"  @click="editOpinion(opinion)">Editar</button>
                            </div>
                        </div>
                    </div>  
                </template>
            </div>
        </div>
    </div>
</template>

<script>
import axios from 'axios'
export default {
    name: 'OpinionView',
    props: [
        'id'
    ],
    data() {
        return {
            game:[],
            opinions: [],
            name: '',
            comentario: '',
            isEditOn: false,
            indexUpdate: '',
            opinionUpdate: '',
        }
    },
    computed: {
        // id() {
        //     return this.$route.params.id;
        // }
    },
    methods: {
        gameDetails() {
            axios
                .get(`https://api.rawg.io/api/games/${this.id}?key=7e07fb9277eb4621be4e3e3f6f69213c`)
                .then((res) => {
                    console.log(res.data);
                    this.game = res.data;
                })
                .catch((error) => {
                console.log(error);
                });
        },
        getPersonalData() {
            const opinionPersona = new Object();
            if ( this.name === '' || this.comentario === '' ) {
                alert('Por favor, llene los 2 campos para agregar su opinión');
            } else {
            opinionPersona.name = this.name;
            opinionPersona.comentario = this.comentario;
            this.opinions.push(opinionPersona);
            this.clearForm();
            }
        },
        deleteOpinion(index) {
            this.opinions.splice(index, 1)
        },
        editOpinion(opinion) {
            this.isEditOn = true;
            this.name = opinion.name;
            this.comentario = opinion.comentario;
            this.opinionUpdate = opinion;
        },
        updateOpinion(){
            this.opinionUpdate.name = this.name;
            this.opinionUpdate.comentario = this.comentario;
            this.isEditOn = false;
        },
        clearForm() {
            this.name = ''
            this.comentario = ''
        },
    },
    created() {
        this.gameDetails();
    }
}
</script>