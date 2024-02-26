<template>
    <div class="movie-detail-overlay" @click="closeDetail">
        <div class="movie-detail-container" @click="closeDetail">
            <v-card>
                <v-card-title style="text-align: center;">
                    {{ movieList.title }}
                </v-card-title>
                <v-img :src="config.url.photo_path + movieList.poster_path"
                    style="height: 400px; width: 100%; object-fit: cover; object-position: center;">
                </v-img>
                <div class="d-flex justify-center ga-2 mt-2">
                    <v-chip v-for="genre in movieList.genres" :key="genre.id">
                        {{ genre.name }}
                    </v-chip>
                </div>
                <v-card-item>
                    <v-card-text>
                        Note:
                    </v-card-text>
                    <v-rating v-model="movieList.vote_average" length="10" color="cyan " half-increments></v-rating>
                    <div class="px-3 ">{{ movieList.vote_count }} votes</div>
                </v-card-item>
                <v-card-item>
                    <v-card-text>
                        Production:
                    </v-card-text>
                    <v-avatar v-for="production in movieList.production_companies" size="64">
                        <v-img :src="config.url.photo_path + production.logo_path" />
                    </v-avatar>
                </v-card-item>
                <v-card-item>
                    <v-card-text>
                        Résumé:
                    </v-card-text>
                    <v-card-text>
                        {{ movieList.overview }}
                    </v-card-text>
                </v-card-item>
            </v-card>
        </div>
    </div>
</template>

<script>
import axios from 'axios';
import config from '@/config.json';

export default {
    name: 'MovieDetail',

    props: {
        movieId: {
            type: Number,
            required: true
        }
    },

    data() {
        return {
            movieList: {},
            config: config
        }
    },

    methods: {
        closeDetail() {
            this.$emit('closeDetail');
        }
    },


    beforeMount() {
        const options = {
            method: 'GET',
            url: config.url.movie_detail + this.movieId,
            params: { language: 'fr-FR' },
            headers: {
                accept: 'application/json',
                Authorization: 'Bearer eyJhbGciOiJIUzI1NiJ9.eyJhdWQiOiI1ZTE2MjVjMzNlOWQ0MWIxMTlkNDcyYjNiNjk5YzVlMyIsInN1YiI6IjY1YzEwMmMyYTM1YzhlMDE2M2Q2NWI5NSIsInNjb3BlcyI6WyJhcGlfcmVhZCJdLCJ2ZXJzaW9uIjoxfQ.Ucy3tzvihJ6dMpfVpZEBNdzL6n_yeLqCnhueekQQZ-k'
            }
        };

        axios
            .request(options)
            .then((response) => {
                this.movieList = response.data;
                console.log(response.data);
            })
            .catch((error) => {
                console.error(error);
            });
    }

}

</script>

<style scoped>
.movie-detail-overlay {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, 0.5);
    /* Arrière-plan semi-transparent */
    display: flex;
    justify-content: center;
    align-items: center;
}

.movie-detail-container {
    background-color: white;
    padding: 10px;
    border-radius: 10px;
    max-width: 90%;
    max-height: 90%;
    overflow: auto;
}
</style>