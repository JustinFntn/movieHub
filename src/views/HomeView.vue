<template>
  <MovieList @showMovieDetail="showMovieDetail" />
  <MovieDetail v-if="show" :movieId="movieId" @closeDetail="closeDetail" />
</template>

<script>
import MovieDetail from '@/components/MovieDetail.vue';
import MovieList from '@/components/MovieList.vue';
import MoviePagination from '@/components/MoviePagination.vue';
import MovieSearch from '@/components/MovieSearch.vue';

export default {
  name: 'HomeView',
  components: {
    MovieList,
    MovieDetail,
    MoviePagination,
    MovieSearch
  },

  data() {
    return {
      movieId: null,
      show: false
    }
  },

  methods: {
    showMovieDetail(id) {
      this.movieId = id;
      this.show = true;
    },

    closeDetail() {
      this.show = false;
    }
  }
}
</script>
