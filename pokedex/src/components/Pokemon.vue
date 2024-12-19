<template>
    <div id="pokemon">
        <div class="card">
            <div class="card-image">
                <figure>
                    <img :src="currentImg" alt="Imagem Pokemon"/>
                </figure>
            </div>
            <div class="card-content">
                <div class="media">                
                    <div class="media-content">
                        <p class="title is-4">{{ num }} - {{ upperName }}</p>
                        <p class="subtitle is-6">{{ pokemon.type }}</p>
                    </div>
                </div>

                <div class="content">
                    <button class="button is-medium is-success is-fllwidth" @click="mudarSprite">
                        Mudar Posição
                    </button>
                </div>
            </div>
        </div>
    </div>
</template>
<script>
    import axios from 'axios';

    export default {
    name: 'PokemonComponent',
    created: function() {
        //console.log(this.url);
        axios.get(this.url)
        .then(response => {
            console.log(response.data);
            this.pokemon.type = response.data.types[0].type.name;
            this.pokemon.frontImg = response.data.sprites.front_default;
            this.pokemon.backImg = response.data.sprites.back_default;
            this.currentImg = this.pokemon.frontImg;
            console.log(this.pokemom);
        });
    },
    data(){
        return {
            isFront: true,
            currentImg: '',
            pokemon: {
                type: '',
                frontImg: '',
                backImg: ''
            }
        }
    },
    props: {
        num: Number,
        name: String,
        url: String
    },
    computed: {
        upperName() {
            return this.name[0].toUpperCase() + this.name.slice(1);
        }
    },
    methods: {
        mudarSprite() {
            if(this.isFront) {
                this.currentImg = this.pokemon.backImg;
                this.isFront = false;
            } else {
                this.currentImg = this.pokemon.frontImg;
                this.isFront = true;
            }
        }
    }
}
</script>


<style>
 #pokemon {
    margin-top: 2%;
 }
</style>