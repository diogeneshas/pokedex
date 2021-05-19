<template>
  <div class="pokemon">

        <div class="card">
        <div class="card-image">
            <figure>
            <img v-bind:src="currentImg" alt="Placeholder image">
            </figure>
        </div>
        <div class="card-content">
            <div class="media">
            <div class="media-content">
                <p class="title is-4">{{num}} {{name}}</p>
                <p class="subtitle is-6">{{ pokemon.type }}</p>
            </div>
            </div>

            <div class="content">
                <button v-on:click="mudarSprite" class="button is-medium is-fullwidth">Mudar Sprite</button>
            </div>
        </div>
        </div>




  </div>
</template>

<script>
import axios from 'axios'

export default {
    created() {
        axios.get(this.url).then(res => {
            this.pokemon.type = res.data.types[0].type.name
            this.pokemon.front = res.data.sprites.front_default
            this.pokemon.back = res.data.sprites.back_default
            this.currentImg = this.pokemon.front
            console.log(this.pokemon)
        })
    },
    data() {
        return {
            pokemon: [],
            isFront: true,
            currentImg: ""
        }
    },
    props: {
        num: Number,
        name: String,
        url: String
    },
    computed: {
        upper(value) {
            var newName = value[0].toUpperCase() +  value.slice(1)
            return newName
        }
    },
    methods: {
        mudarSprite() {
            if(this.isFront) {
                this.isFront = false
                this.currentImg = this.pokemon.back
            } else {
                this.isFront = true
                this.currentImg = this.pokemon.front
            }
        }
    }
}
</script>

<style>
    .pokemon {
        padding: 1%;
    }
</style>