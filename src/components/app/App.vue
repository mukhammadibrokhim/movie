<template>
  <div class="app font-monospace">
      <div class="content">
        <AppInfo  :allMoviesCount="movies.length" :favouriteMvoiesCount="movies.filter(c => c.favourite).length"/>
        <div class="search-panel shadow">
          <SearchPanel/>
          <AppFilter/>
      </div>
      <MoveList :movies="movies" @onToggle="onToggleHandler"/>
      <MovieAddForm  @createMovie="createMovie"/>
    </div>
  </div>
 
</template>

<script>
import  AppInfo from '@/components/app-info/AppInfo.vue'
import SearchPanel from '@/components/search-panel/SearchPanel.vue'
import AppFilter from '@/components/app-filter/AppFilter.vue'
import MoveList from '@/components/movie-list/MovieList.vue'
import MovieAddForm from '@/components/movie-add-form/MovieAddForm.vue'
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
            movies: [
                {
                    id:1,
                    name: 'Omar', 
                    viewers: 811,
                    favourite: false,
                    like: true
                },
                {
                    id:2, 
                    name: 'Empire of Osman', 
                    viewers: 711,
                    favourite: true,
                    like: false
                },
                {
                    id:3,
                    name: 'Ertugrul', 
                    viewers: 411,
                    favourite: false,
                    like: false
                }
                
            ]
        }
    },

    methods: {
      createMovie(item){
        this.movies.push(item)
      },

      onToggleHandler({id,prop}){
        this.movies = this.movies.map(item => {
          if(item.id == id){
            return {... item, [prop]: !item[prop]}
          }
          return item
        })
      },
      
    },

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