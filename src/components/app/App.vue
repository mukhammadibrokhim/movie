<template>
  <div class="app">
  <div class="content">
    <AppInfo />
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
</style>