<template>
    <ul class="movie-list list-group">
      
      <MovieListItem v-for="movie in movies" :movie="movie"/>
    
    </ul>
</template>
<script>
import MovieListItem from '../movieListItem/MovieListItem.vue';

export default { components: { MovieListItem },
data(){
    return {
        movies: [
            {
                name:'Omar',
                viewers:911,
                favourite:false,
                like:true,
            },
            {
                name:'Ertugrul',
                viewers:711,
                favourite:false,
                like:false,
            },
            {
                name:'Empire of osmon',
                viewers:811,
                favourite:true,
                like:false,
            },
        ]
    }
} }

</script>
<style scoped>
.movie-list {
    margin-top: 2rem;
    padding: 1.5rem;
    background-color: #fcfaf5;
    border-radius: 4px;
    box-shadow: 15px 15px 15px rgba(0, 0, 0, 0.15);

}
</style>