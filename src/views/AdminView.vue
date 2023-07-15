<template>
    <div>
        <div v-if="name == '' || lastName == ''">
            <h1>Para ver la información debe ingresar sus datos</h1>
            <button class="btn btn-dark" @click="getName()">Ingresar Datos</button>
        </div>
        <div v-else>
            <div class="col-md-2">
                <svg xmlns="http://www.w3.org/2000/svg" class="icon icon-tabler icon-tabler-user" width="44" height="44" viewBox="0 0 24 24" stroke-width="1.5" stroke="#000000" fill="none" stroke-linecap="round" stroke-linejoin="round">
                    <path stroke="none" d="M0 0h24v24H0z" fill="none"/>
                    <path d="M8 7a4 4 0 1 0 8 0a4 4 0 0 0 -8 0" />
                    <path d="M6 21v-2a4 4 0 0 1 4 -4h4a4 4 0 0 1 4 4v2" />
                </svg>
                <h2>Bienvenido/a! {{ name }} {{ lastName }}</h2>
            </div>
            <div class="col-md-5 container">
                <h3>Resumen de tu cuenta</h3>
                <h4>Le diste me gusta al juego <strong>{{ game.name }} </strong></h4>
                <div class="border border-dark p-3">
                    <h5 class="mt-2 mb-5">¿Deseas comprar coins para este juego?</h5>
                    <button class="btn btn-warning mb-2 " @click="coins++; fillProgressBar()" id="btn-coins">Agregar coins</button>
                    <h3 class="border-top border-dark border-opacity-50 pt-3 mt-2">Cantidad de coins compradas</h3>
                    <div class="progress">
                        <div :class="colorProgressBar" role="progressbar" aria-label="Success example" :style="percentCoins" aria-valuenow="25" aria-valuemin="0" aria-valuemax="100">
                            <span class="text-light">$ {{ coins }} </span>
                        </div>
                    </div>
                    <h3 v-if="coins >= 50" class="my-3">Llegaste al máximo de tu crédito</h3>
                </div>
                <div class="row mt-3">
                    <table class="table">
                        <thead>
                            <th class="bg-warning"><h3>% de finalización de juego</h3></th>
                            <th class="bg-success"><h3 class="text-light">Logros en el juego</h3></th>
                            <th class="bg-info"><h3>Recompensas</h3></th>
                        </thead>
                        <tbody  >
                            <td class="bg-warning"><h3>17% <svg xmlns="http://www.w3.org/2000/svg" class="icon icon-tabler icon-tabler-star-half" width="44" height="44" viewBox="0 0 24 24" stroke-width="1.5" stroke="#000000" fill="none" stroke-linecap="round" stroke-linejoin="round">
                                <path stroke="none" d="M0 0h24v24H0z" fill="none"/>
                                <path d="M12 17.75l-6.172 3.245l1.179 -6.873l-5 -4.867l6.9 -1l3.086 -6.253z" />
                                </svg></h3></td>
                            <td class="bg-success"><h3 class="text-light">166<svg xmlns="http://www.w3.org/2000/svg" class="icon icon-tabler icon-tabler-trophy" width="44" height="44" viewBox="0 0 24 24" stroke-width="1.5" stroke="#ffffff" fill="none" stroke-linecap="round" stroke-linejoin="round">
                                <path stroke="none" d="M0 0h24v24H0z" fill="none"/>
                                <path d="M8 21l8 0" />
                                <path d="M12 17l0 4" />
                                <path d="M7 4l10 0" />
                                <path d="M17 4v8a5 5 0 0 1 -10 0v-8" />
                                <path d="M5 9m-2 0a2 2 0 1 0 4 0a2 2 0 1 0 -4 0" />
                                <path d="M19 9m-2 0a2 2 0 1 0 4 0a2 2 0 1 0 -4 0" />
                                </svg></h3></td>
                            <td class="bg-info"><h3>200<svg xmlns="http://www.w3.org/2000/svg" class="icon icon-tabler icon-tabler-medal" width="44" height="44" viewBox="0 0 24 24" stroke-width="1.5" stroke="#000000" fill="none" stroke-linecap="round" stroke-linejoin="round">
                            <path stroke="none" d="M0 0h24v24H0z" fill="none"/>
                            <path d="M12 4v3m-4 -3v6m8 -6v6" />
                            <path d="M12 18.5l-3 1.5l.5 -3.5l-2 -2l3 -.5l1.5 -3l1.5 3l3 .5l-2 2l.5 3.5z" />
                            </svg></h3></td>
                        </tbody>
                    </table>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import axios from 'axios'

export default {
    name: 'AdminView',
    props: [
        'id'
    ],
    data() {
        return {
            name: '',
            lastName: '',
            game:[],
            coins: 0,
            percentCoins: '',
            colorProgressBar: 'progress-bar bg-success',
        }
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
        getName() {
            let name = prompt('Por favor ingrese su nombre');
            if (name === '' || name === null) {
                alert('Por favor ingrese un nombre válido');
                this.getName();
            } else {
                this.name = name;
                this.getLastName();
            }
        }, 
        getLastName() {
            let lastName = prompt('Ingrese su apellido');
            if (lastName === '' || lastName === null) {
                alert('Por favor ingrese un apellido válido');
                this.getLastName();
            } else {
                this.lastName = lastName;
            }
        },
        fillProgressBar(){
            this.percentCoins = `width: ${this.coins*2}%`
            if ( this.coins > 20) {
                this.colorProgressBar = `progress-bar bg-warning`
            }
            if ( this.coins > 30) {
                this.colorProgressBar = `progress-bar bg-danger`
            }
            if ( this.coins >= 50) {
                this.coins = 50;
                let botonCoins = document.getElementById('btn-coins');
                botonCoins.setAttribute('disabled', '');
            }
        }
    },
    created() {
        this.gameDetails();
    }
}
</script>

