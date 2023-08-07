<template>
  <div class="app font-monospace">
    <!-- <button @click="fetchData()">Click</button> -->
    <div class="content">
      <AppInfo :allMoviesCount='movies.length' :favouriteMoviesCount="movies.filter(c => c.favourite).length" />
      <div class="search-panel">
        <SearchPanel :updateTermHandler="updateTermHandler" />
        <AppFilter :updateFilterHandler="updateFilterHandler" :filterName="filter" />
      </div>

      <Box v-if="!movies.length && !isLoading">
        <h1>Kinolar yo'q</h1>
      </Box>

      <Box v-else-if="isLoading" class="d-flex justify-content-center">
        <Loader />
      </Box>

      <MovieList v-else :movies="onFilterHandler(onSearchHandler(movies, term), filter)" @onToggle="onToggleHandler"
        @onRemove='onRemoveHandler' />
      <Box class="d-flex justify-content-center">
        <nav aria-label="pagination">
          <ul class="pagination pagination-sm">
            <li @click="changePageHandler(pageNum)" key="pageNum" :class="{ active: pageNum === page }"
              aria-current="page" v-for="pageNum in totalPage">
              <span class="page-link">{{ pageNum }}</span>
            </li>
          </ul>
        </nav>
      </Box>
      <MovieAddForm @createMovie='createMovie' />
    </div>
  </div>
</template>
<script>

import AppInfo from '@/appInfo/AppInfo.vue';
import SearchPanel from '@/search-panel/SearchPanel.vue';
import AppFilter from '@/appFilter/AppFilter.vue';
import MovieList from '@/movieList/MovieList.vue';
import MovieAddForm from '@/movieAddForm/MovieAddForm.vue';
import axios from 'axios';

export default {
  components: {
    AppInfo,
    SearchPanel,
    AppFilter,
    MovieList,
    MovieAddForm,

  },
  data() {
    return {
      movies: [],
      term: '',
      filter: 'all',
      isLoading: false,
      page: 1,
      limit: 10,
      totalPage: 0
    }

  },
  methods: {

    createMovie(item) {
      try {
        const response = axios.post("https://jsonplaceholder.typicode.com/posts", item)
        this.movies.push(response.data)
      } catch (error) {
        alert(error.message)
      }
    },

    onToggleHandler({ id, prop }) {
      this.movies = this.movies.map(item => {
        if (item.id === id) {
          return { ...item, [prop]: !item[prop] };
        }
        return item
      })
    },

    async onRemoveHandler(id) {
      try {
        const response = await axios.delete(`https://jsonplaceholder.typicode.com/posts/${id}`)
        this.movies = this.movies.filter(c => c.id !== id)
      } catch (error) {
        alert(error.message)
      }

    },

    onSearchHandler(arr, term) {
      if (term.length === 0) {
        return arr
      }
      return arr.filter(c => c.name.toLowerCase().indexOf(term) > -1)
    },

    onFilterHandler(arr, filter) {
      switch (filter) {
        case 'popular':
          return arr.filter(c => c.like)
        case 'mostViewers':
          return arr.filter(c => c.viewers > 500)
        default:
          return arr
      }
    },

    updateTermHandler(term) {
      this.term = term
    },

    updateFilterHandler(filter) {
      this.filter = filter
    },

    // logger() {
    //   console.log("Mounted");
    // },
    // mounted() {
    //   this.logger()
    // },
    // updadeLog() {
    //   console.log('updated');
    // },

    // updated() {
    //   this.updadeLog()
    // },
    async fetchData() {
      try {
        this.isLoading = true
        const response = await axios.get("https://jsonplaceholder.typicode.com/posts", {
          params: {
            _limit: this.limit,
            _page: this.page
          }
        })
        const newArr = response.data.map(el => ({
          id: el.id,
          name: el.title,
          viewers: el.id * 10,
          like: false,
          favourite: false
        }))
        this.totalPage = Math.ceil(response.headers['x-total-count'] / this.limit)
        this.movies = newArr
        console.log(this.totalPage);
      } catch (error) {
        alert(error.message)
      } finally {
        this.isLoading = false
      }
    },
    changePageHandler(page) {
      this.page = page

    },
  },
  mounted() {
    this.fetchData()
  },
  watch: {
    page() {
      this.fetchData()
    }
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
