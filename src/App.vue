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
          color="pink"
          dark
          @click.stop='toggleCart()'
        >
          Toggle
        </v-btn>
    </v-app-bar>
    <v-navigation-drawer
      v-model="cartDrawer"
      absolute
      temporary
      right
    >
      <v-list-item>
        <v-list-item-avatar>
          <v-img src="https://randomuser.me/api/portraits/men/78.jpg"></v-img>
        </v-list-item-avatar>

        <v-list-item-content>
          <v-list-item-title>John Leider</v-list-item-title>
        </v-list-item-content>
      </v-list-item>

      <v-divider></v-divider>

      <v-list dense>
        <v-list-item
          v-for="item in items"
          :key="item.title"
          link
        >
          <v-list-item-icon>
            <v-icon>{{ item.icon }}</v-icon>
          </v-list-item-icon>

          <v-list-item-content>
            <v-list-item-title>{{ item.title }}</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>
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
      item: [],
      cartDrawer: null,
      items: [
        { title: 'Home', icon: 'mdi-view-dashboard' },
        { title: 'About', icon: 'mdi-forum' },
        ],
    }
  },
  created () {
    this.getItem()
  },
  mounted () {
    
  },
  methods: {
    toggleCart() {
      this.cartDrawer = !this.cartDrawer
      console.log(this.cartDrawer);
    },
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
