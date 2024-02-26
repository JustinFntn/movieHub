<template>
    <div>
        <v-text-field v-model="search" append-icon="mdi-magnify" label="Search" single-line hide-details
            placeholder="search"></v-text-field>
    </div>
</template>

<script>
export default {
    name: 'MovieSearch',

    watch: {
        search(val) {
            this.$emit('searchMovieEmit', val);
        }
    },
}

</script>