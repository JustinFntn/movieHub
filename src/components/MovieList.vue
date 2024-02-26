<template>
    <v-container fluid>
        <v-row justify="center">
            <v-col v-for="movie in movielist.results" sm="6" md="3" xs="12">
                <Movie :movie="movie" @click="showMovieDetailEmit(movie.id)" />
            </v-col>
        </v-row>
    </v-container>
</template>

<script>
import axios from 'axios';
import Movie from '@/components/Movie.vue';
import config from '@/config.json';

export default {
    name: 'MoviesList',

    components: {
        Movie
    },

    data() {
        return {
            movielist: [],
        }
    },

    methods: {
        showMovieDetailEmit(id) {
            this.$emit('showMovieDetail', id);
        }
    },

    beforeMount() {

        const options = {
            method: 'GET',
            url: 'https://api.themoviedb.org/3/discover/movie',
            params: {
                include_adult: 'false',
                include_video: 'false',
                language: 'fr-FR',
                sort_by: 'popularity.desc'
            },
            headers: {
                accept: 'application/json',
                Authorization: 'Bearer eyJhbGciOiJIUzI1NiJ9.eyJhdWQiOiI1ZTE2MjVjMzNlOWQ0MWIxMTlkNDcyYjNiNjk5YzVlMyIsInN1YiI6IjY1YzEwMmMyYTM1YzhlMDE2M2Q2NWI5NSIsInNjb3BlcyI6WyJhcGlfcmVhZCJdLCJ2ZXJzaW9uIjoxfQ.Ucy3tzvihJ6dMpfVpZEBNdzL6n_yeLqCnhueekQQZ-k'
            }
        };

        axios
            .request(options)
            .then((response) => {
                this.movielist = response.data;
            })
            .catch((error) => {
                console.error(error);
            });
    },
}

</script>