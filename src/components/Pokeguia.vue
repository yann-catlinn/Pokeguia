<template>
<div class="container my-3">
    <div class="row">
        <div class="col-lg-12 mt-5">
            <img  src="src/img/logo.png" alt="logo_pokemon" class="mx-auto d-block">
        </div>
    </div>
    <div class="row">
        <div class="col-lg-12">
            <h1 class="text-center mt-5">PokeGuía</h1>
            <div class="flex-row">
                <p class="text-center mt-4">Ingresa el nombre del personaje</p>
                <div class="d-flex justify-content-center ">

                    <div class="input-group mb-3 col-md-4">
                        <label>Nombre:</label>
                        <input type="text" v-model="character.name" @keyup.enter="fetchCharacter" class="form-control" placeholder="Ingrese nombre del personaje">
                        <div class="input-group-append">
                            <button @click.prevent="fetchCharacter" class="btn btn-outline-secondary" type="button">Buscar</button>
                        </div>
                    </div>
                </div>
                <img :src="image.front_default" alt="foto pokemon" class="mx-auto d-block">
                <h3 class="text-center">Movimientos</h3>
                <ul class="lista_caracteristicas">
                    <li v-for="(movimiento,index) in movimientos" :key="index">{{movimiento.move.name}}</li>
                </ul>
                <h3 class="text-center">Habilidades</h3>
                <ul class="lista_caracteristicas ">
                    <li v-for="(habilidad,index) in habilidades" :key="index">{{habilidad.ability.name}}</li>
                </ul>
            </div>

        </div>

    </div>
</div>
</template>

<script>
export default {
    name: 'data_pokemon',
    //props: {},
    data: function () {
        return {
            character: {
                name: "pikachu",
                moves: "",
                abilities: "",
                sprites: {
                    front_default: "",
                },
            },
        }
    },
    computed: {
        image() {
            return this.character.sprites;
        },
        movimientos() {
            return this.character.moves;
        },
        habilidades() {
            return this.character.abilities;
        }
    },
    methods: {
        fetchCharacter() {
            fetch(`https://pokeapi.co/api/v2/pokemon/${this.character.name}`)
                .then(response => response.json())
                .then(json => {
                    console.log(json);
                    this.character = json;
                })
                .catch(error => {
                    alert("¿Quién es ese Pokemón? Intenta nuevamente");
                    console.log(error);
                })
        },
    },
    // components: {},
    created() {
        this.fetchCharacter();
    }
}
</script>

<style scoped>
.lista_caracteristicas {
    column-count: 6;
}
</style>
