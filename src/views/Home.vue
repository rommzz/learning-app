<template>
  <v-container>
    <v-card
      flat
      class="py-12"
    >
      <v-card-text>
        <v-row
          align="center"
          justify="center">
          <v-btn-toggle
            color="red darken-1">
            <v-btn v-for="(item, index) in summary" :key="index">
              <div white--text>
                {{item}}
              </div>
            </v-btn>
          </v-btn-toggle>
        </v-row>
      </v-card-text>
    </v-card>
    <v-row no-gutters>
      <v-col>
        
      </v-col>
    </v-row>
    <v-row class="text-center">
      <v-col cols="6" sm="4" md="4" lg="3" xl="2"  v-for="(data, index) in item" :key="index">
        <v-card
          class="mx-auto"
          max-width="344">
          <v-list-item-avatar
            tile
            size="100"
            color="grey">
            <v-img
              :aspect-ratio="1/1"
              width="100%"
              :src="data.image_url"
            ></v-img>
            </v-list-item-avatar>
          <v-list-item three-line>
            <v-list-item-content>
              <div class="d-flex ">
                <div class=" mr-1 pa-1" style="border-radius: 4px; border: 1px solid #047bf8; color: #047bf8">
                  {{ data.category }}
                </div>
                <div v-if="data.is_free" class="pa-1" style="border-radius: 4px; border: 1px solid #22b315; color: #22b315">
                  {{'Free ' + data.max_purchase + ' item/day' }}
                </div>
              </div>
              <v-list-item-title class="headline d-flex mb-1" style="font-size: 16px!important">
                {{ data.name }}
              </v-list-item-title>
              <v-list-item-subtitle>{{'Rp. ' + data.base_price }}</v-list-item-subtitle>
            </v-list-item-content>
          </v-list-item>

          <!-- <v-card-actions>
            <v-btn
              outlined
              rounded
              text
            >
              Button
            </v-btn>
          </v-card-actions> -->
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import axios from "axios";
export default {
  name: 'Home',

  data (){
    return{
      item: [],
      summary: []
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
        this.summary = response.data.summary
        this.item = response.data.data
        console.log(this.summary);
        
      })
      .catch(function (error) {
        // handle error
        console.log(error);
      })
    }
  }
}
</script>
