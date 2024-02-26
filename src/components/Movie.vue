<template>
    <v-container>
        <v-col>
            <v-card class="card" width="200" hover>
                <v-img :src="config.url.photo_path + movie.poster_path"></v-img>
                <v-card-title>{{ movie.title }}</v-card-title>
                <v-card-subtitle>{{ movie.overview }}</v-card-subtitle>
            </v-card>
        </v-col>
    </v-container>
</template>

<script>
import config from '@/config.json';

export default {
    name: 'Movie',
    props: {
        movie: {
            type: Object,
            required: true
        }
    },

    data() {
        return {
            config: config,
            reveal: false
        }
    },


    beforeMount() {

        // console.log(this.movie);
    }
}
</script>

<style></style>