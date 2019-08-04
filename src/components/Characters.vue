<template>
    <v-container>
        <h3>Characters</h3>
        <ul>
            <li v-for="character in characters" :key="character.id">
                {{ character.description }}
            </li>
        </ul>
    </v-container> 
</template>

<script>
import { public_key, secret_key } from '../marvel';
import axios from 'axios';

export default {
    name: "Characters",
    data: () => ({
        characters: [],
        item: []

    }),
    mounted(){
        this.getCharacters();
    },
    methods: {
        getCharacters: function() {
            axios.get(`http://gateway.marvel.com/v1/public/characters?apikey=${public_key}`)
            .then((result) => {
                console.log(result)
                result.data.data.results.forEach((item) => {
                    this.characters.push(item) 
                    })
                })
            .catch((error) => {
                console.log(error)
            })
        }
    }
}
</script>

<style>
  
</style>
