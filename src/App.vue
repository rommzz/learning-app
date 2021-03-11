<template>
  <v-app>
    <v-app-bar
      app
      color="white"
      dark
    >
      <div class="d-flex align-center">
        <v-img
          src="https://glovory-mart.netlify.app/icons/logo-color.svg"
          contain
          height="50"
        />
        <v-autocomplete
          clearable
          dense
          solo
          flat
          hide-details=true
          label="search product..."
        ></v-autocomplete>
      </div>

      <v-spacer></v-spacer>

      <v-btn
        href="https://github.com/vuetifyjs/vuetify/releases/latest"
        target="_blank"
        text
      >
        <span class="mr-2 black--text">Latest Release</span>
        <v-icon color="black">mdi-plus</v-icon>
      </v-btn>
    </v-app-bar>

    <v-main>
      <Home/>
    </v-main>
  </v-app>
</template>

<script>
import Home from './views/Home';
import axios  from "axios";

export default {
  name: 'App',

  components: {
    Home,
  },
  data (){
    return{
      item: []
    }
  },
  created () {
    this.getItem()
  },
  mounted () {
    
  },
  methods: {
    getItem(){
      axios.get('https://glovorymart.glitch.me/api/products')
      .then((response) => {
        // handle success
        this.item = response
        console.log(this.item);
        
      })
      .catch(function (error) {
        // handle error
        console.log(error);
      })
    }
  }
};
</script>
