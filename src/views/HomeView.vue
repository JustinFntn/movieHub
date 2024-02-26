<template>
  <MovieList />
</template>

<script>
import MovieDetail from '@/components/MovieDetail.vue';
import MovieList from '@/components/MovieList.vue';
import MoviePagination from '@/components/MoviePagination.vue';
import MovieSearch from '@/components/MovieSearch.vue';
import config from '@/config.json';

export default {
  name: 'HomeView',
  components: {
    MovieList,
    MovieDetail,
    MoviePagination,
    MovieSearch
  },
}

</script>
