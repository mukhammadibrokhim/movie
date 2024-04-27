<template>
  <div class="app">
    <div class="content">
      <AppInfo />
    </div>
    <div class="search-panel">
      
    </div>
  </div>
 
</template>

<script>
import  AppInfo from '@/components/app-info/AppInfo.vue'
  export default {
    components: {
      AppInfo,
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