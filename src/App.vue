<template>
  <v-app>
    <v-main>
      <div id="app">
        <Header />
        <Defuncts v-bind:defuncts="defuncts" />
      </div>
    </v-main>
  </v-app>
</template>

<script>
import Header from './components/Header.vue';
import Defuncts from './components/Defuncts.vue';
import axios from 'axios';
//const fileNumber = () => Math.floor(Math.random() * (2)); 
//const DefunctsDataFile = `assets/data/def${fileNumber()}.json`;
const DefunctsDataFile = 'assets/data/def1.json';
console.log(DefunctsDataFile);
//import DefunctsData from eval('assets/data/def'+fileN+'.json');

export default {
  name: 'App',
  components: {
    Header,
    Defuncts
  },
  data() {
    return  {
      defuncts: []
      //defuncts: DefunctsData
    }
  },
    created() {
      axios.get(DefunctsDataFile)
      .then(res => this.defuncts = res.data)
      .catch(err => console.log(err))
    
    }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #ddd;
  padding-top: 60px;
  background-color: #242628;
}
body {
  background-color: #242628;
}
</style>