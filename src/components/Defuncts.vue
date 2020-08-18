<template>
  <v-container>
    <v-row class="text-center">
      <v-col cols="12">
        <div>
          <div v-bind:key="defunct.ID_REGISTRO" v-for="defunct in defuncts"> 
            <DefunctItem v-bind:defunct="defunct"/>
          <!--<div v-bind:key="defuncts[defunctNumber].ID_REGISTRO">  
            <DefunctItem v-bind:defunct="defuncts[defunctNumber]"/>-->
          </div>
        </div>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import DefunctItem  from './DefunctItem.vue';

export default {
  name: 'Defuncts',
  components: {
    DefunctItem
  },
  data() {
    return {
      defunctNumber: this.randomNumber()
    }
  },
  props: ["defuncts"],
  methods : {
    randomNumber : function(){
      return Math.floor(Math.random() * (10));
    }
  }
}
</script>

<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
