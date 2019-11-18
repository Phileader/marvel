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
    <v-card
      class="mx-auto"
      max-width="500"
    >
      <v-system-bar
        color="indigo darken-2"
        dark
      >
        <v-spacer></v-spacer>
  
        <v-icon>mdi-window-minimize</v-icon>
  
        <v-icon>mdi-window-maximize</v-icon>
  
        <v-icon>mdi-close</v-icon>
      </v-system-bar>
  
      <v-toolbar
        color="indigo"
        dark
      >
        <v-app-bar-nav-icon></v-app-bar-nav-icon>
  
        <v-toolbar-title>Discover</v-toolbar-title>
  
        <v-spacer></v-spacer>
  
        <v-btn icon>
          <v-icon>mdi-magnify</v-icon>
        </v-btn>
      </v-toolbar>
  
      <v-container fluid>
        <v-row dense>
          <v-col
            v-for="card in tabImagesCharacters"
            :key="card.name"
            :cols= 6
          >
            <v-card>
                
              <v-img
                :src="card.src"
                class="white--text align-end"
                gradient="to bottom, rgba(0,0,0,.1), rgba(0,0,0,.5)"
              >
                <v-card-title v-text="card.name"></v-card-title>
              </v-img>
  
              <v-card-actions>
                <v-spacer></v-spacer>
  
                <v-btn icon>
                  <v-icon>mdi-heart</v-icon>
                </v-btn>
  
                <v-btn icon>
                  <v-icon>mdi-bookmark</v-icon>
                </v-btn>
  
                <v-btn icon>
                  <v-icon>mdi-share-variant</v-icon>
                </v-btn>
              </v-card-actions>
            </v-card>
          </v-col>
        </v-row>
      </v-container>
    </v-card>

    </v-app> 
</template>

<script>
import { public_key, secret_key } from '../marvel';
import axios from 'axios';

export default {
    name: "Characters",
    data: () => ({
        characters: [],
        item: [],
        cards: [
            { title: 'Pre-fab homes', src: 'https://cdn.vuetifyjs.com/images/cards/house.jpg', flex: 12 },
            { title: 'Favorite road trips', src: 'http://i.annihil.us/u/prod/marvel/i/mg/c/e0/535fecbbb9784/portrait_xlarge.jpg', flex: 6 },
            { title: 'Best airlines', src: 'http://i.annihil.us/u/prod/marvel/i/mg/c/e0/535fecbbb9784/portrait_xlarge.jpg', flex: 6 },
        ],
        tabImagesCharacters: []
    }),
    mounted(){
        this.getCharacters();
    },
    methods: {
        getCharacters: function() {
            axios.get(`https://gateway.marvel.com/v1/public/characters?limit=20&offset=0&apikey=${public_key}`)
            .then((result) => {
                //console.log(result)
                result.data.data.results.forEach((item) => {
                        this.characters.push(item) 
                        this.tabImagesCharacters.push({
                            'name' : item.name,
                            'src' :  item.thumbnail.path + '/portrait_xlarge.' + item.thumbnail.extension
                        })
                    })
                })
            .catch((error) => {
                console.log(error)
            })
            //console.log(this.tabImagesCharacters);
        }
    }
}
</script>

<style>
  
</style>
