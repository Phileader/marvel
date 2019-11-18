<template>
    <v-app>
        <v-container>
            <h3>Events</h3>
            <ul>
                <li v-for="event in events" :key="event.id">
                    {{ event.title }}
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
        events: [],
        item: []
    }),
    mounted(){
        this.getEvents();
    },
    methods: {
        getEvents: function() {
            axios.get(`http://gateway.marvel.com/v1/public/events?limit=10&offset=0&apikey=${public_key}`)
            .then((result) => {
                console.log(result)
                result.data.data.results.forEach((item) => {
                        this.events.push(item) 
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
