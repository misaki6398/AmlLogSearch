﻿<template>
  <div id="app">
      <div class="container">
        <navbar></navbar>
        
      </div>  
      <router-view></router-view>   
      
  </div>
</template>

<script>
import navbar from '@/components/Header/NavBar'
export default {
  name: 'app',
  data () {
    return {
      test: ""
    }
  },
  components: {
    navbar
  } 
}

</script>
