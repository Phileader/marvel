<template>
    <v-app>
        <v-container>
            <h3>Characters</h3>
            <ul>
                <li v-for="character in characters" :key="character.id">
                    {{ character.name }}
                </li>
            </ul>
        </v-container>
    </v-app> 
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
            axios.get(`http://gateway.marvel.com/v1/public/characters?limit=40&offset=0&apikey=${public_key}`)
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
