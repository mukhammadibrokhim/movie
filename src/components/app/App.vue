<template>
  <div class="app font-monospace">
    <div class="content">
      <AppInfo :allMoviesCount="movies.length" :favouriteMvoiesCount="movies.filter(c => c.favourite).length" />
      <div class="search-panel shadow">
        <SearchPanel :updateTermHandler="updateTermHandler" />
        <AppFilter :updateFilterHandler="updateFilterHandler" :filterName="filter" />
      </div>
      <Box v-if="!movies.length && !isLoading">
        <p class="text-center fs-3 text-danger">Kinolar yo'q!</p>
      </Box>
      <Box v-else-if="isLoading" class=" d-flex justify-content-center">
        <Loader/>
      </Box>
      <MoveList v-else :movies="onFilterHandler(onSearchHandler(movies, term), filter)" @onToggle="onToggleHandler" @onRemove="onRemoveHandler" />
      <!-- pagination -->
      <Box class="d-flex justify-content-center">
        <nav aria-label="pagination">
          <ul class="pagination pagination-sm">
            <li v-for="pageNuber in totalPages" :key="pageNuber" :class="{'active': pageNuber == page}" @click="changePageHandler(pageNuber)">
              <span class="page-link">{{ pageNuber }}</span>
            </li>
          </ul>
        </nav>
      </Box>
      <!--  -->
      <MovieAddForm @createMovie="createMovie" />
    </div>
  </div>
</template>

<script>
  import AppInfo from '@/components/app-info/AppInfo.vue'
  import SearchPanel from '@/components/search-panel/SearchPanel.vue'
  import AppFilter from '@/components/app-filter/AppFilter.vue'
  import MoveList from '@/components/movie-list/MovieList.vue'
  import MovieAddForm from '@/components/movie-add-form/MovieAddForm.vue'
  import axios from 'axios'
  export default {
    components: {
      AppInfo,
      SearchPanel,
      AppFilter,
      MoveList,
      MovieAddForm,
    },
    data() {
      return {
        movies: [],
        term: '',
        filter: '',
        isLoading: false,
        limit: 10,
        page: 1,
        totalPages: 0,
      }
    },
    methods: {
      createMovie(item) {
        this.movies.push(item)
      },
      onToggleHandler({
        id,
        prop
      }) {
        this.movies = this.movies.map(item => {
          if (item.id == id) {
            return { ...item,
              [prop]: !item[prop]
            }
          }
          return item
        })
      },
      onRemoveHandler(id) {
        this.movies = this.movies.filter(c => c.id !== id)
      },
      onSearchHandler(arr, term) {
        if (term.length == 0) {
          return arr;
        }
        return arr.filter(c => c.name.toLowerCase().indexOf(term) > -1)
      },
      onFilterHandler(arr, filter) {
        switch (filter) {
          case 'popular':
            return arr.filter(c => c.like);
          case 'mostViews':
            return arr.filter(c => c.viewers > 500)
          default:
            return arr;
        }
      },
      updateTermHandler(term) {
        this.term = term
      },
      updateFilterHandler(filter) {
        this.filter = filter
      },
      async fetchMvoie() {
        try {
          this.isLoading = true;
          const response = await axios.get('https://jsonplaceholder.typicode.com/posts', {
            params: {
              _limit: this.limit,
              _page: this.page,
            }
          })
          const newArr = response.data.map(item => ({
            id: item.id,
            name: item.title,
            like: false,
            favourite: false,
            viewers: item.id * 10
          }))
          this.totalPages = Math.ceil(response.headers['x-total-count'] / this.limit);
          this.movies = newArr
          console.log(this.totalPages)
        } catch (e) {
          alert(e.message)
        } finally {
          this.isLoading = false;
        }
      },

      changePageHandler(page){
        this.page = page
        this.fetchMvoie()
      },

    },
    mounted() {
      this.fetchMvoie()
    }
  }
</script>

<style>
  .app {
    height: 100vh;
    color: black;
  }
  .content {
    width: 1000px;
    min-height: 700px;
    background-color: #fff;
    margin: 0 auto;
    padding: 5rem 0
  }
  .search-panel {
    margin-top: 2rem;
    padding: 1.5rem;
    background-color: #fcfaf5;
    border-radius: 4px;
    box-shadow: 15px, 15px, 15px rgba(0, 0, 0, 0.15);
  }
</style>