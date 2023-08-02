<template>
  <div class="app font-monospace">
    <div class="content">
      <AppInfo :allMoviesCount='movies.length' :favouriteMoviesCount="movies.filter(c => c.favourite).length" />
      <div class="search-panel">
        <SearchPanel />
        <AppFilter />
      </div>
      <MovieList :movies="movies" @onToggle="onToggleHandler" />
      <MovieAddForm @createMovie='createMovie' />
    </div>
  </div>
</template>
<script>

import AppInfo from '@/appInfo/AppInfo.vue';
import SearchPanel from '../search-panel/SearchPanel.vue';
import AppFilter from '../appFilter/AppFilter.vue';
import MovieList from '../movieList/MovieList.vue';
import MovieAddForm from '../movieAddForm/MovieAddForm.vue';

export default {
  components: {
    AppInfo,
    SearchPanel,
    AppFilter,
    MovieList,
    MovieAddForm
  },
  data() {
    return {
      movies: [
        {
          name: 'Omar',
          viewers: 911,
          like: true,
          favourite: false,
          id: 1
        },
        {
          name: 'Ertugrul',
          viewers: 711,
          like: false,
          favourite: false,
          id: 2
        },
        {
          name: 'Empire of osmon',
          viewers: 811,
          like: true,
          favourite: true,
          id: 3
        },
      ]
    }

  },
  methods: {
    createMovie(item) {
      this.movies.push(item)
    },
    onToggleHandler({ id, prop }) {
      this.movies = this.movies.map(item => {
        if (item.id === id) {
          return { ...item, [prop]: !item[prop] };
        } 
        return item
      })
    },
  }
}
</script>
<style>
.app {
  height: 100vh;
  color: #000;
}

.content {
  width: 1000px;
  min-height: 700px;
  background-color: #fff;
  margin: 0 auto;
  padding: 5rem 0;
}

.search-panel {
  margin-top: 2rem;
  padding: 1.5rem;
  background-color: #fcfaf5;
  border-radius: 4px;
  box-shadow: 15px 15px 15px rgba(0, 0, 0, 0.15);
}
</style>
