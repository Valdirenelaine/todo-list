<template>
<v-app id="app">
   <NavBar> </NavBar>
   <v-main>
     <v-container>
        <Home></Home>
     </v-container>
   </v-main>
</v-app>
</template>

<script>
import NavBar from './components/NavBar.vue'
import Home from './components/Home.vue'

export default {
  name: 'App',
  components: {
    NavBar,
    Home

  }
}
</script>
 
