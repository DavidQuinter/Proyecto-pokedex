<template>
  <div>
    <div class="logo">
      <img src="//cdn2.bulbagarden.net/upload/4/4b/Pok%C3%A9dex_logo.png">
    </div>

    <div class="content">
      <div v-for="(data, index) in pokemons" :key="index">
        <v-app id="inspire">
          <v-card
            class="mx-auto"
            max-width="344"
          >
            <v-img
              class="mano"
              :src="data.url"
              height="200px"
            ></v-img>
        
            <v-card-title>
              {{ data.name }}
            </v-card-title>

            <v-card-subtitle>
              1,000 miles of wonder
            </v-card-subtitle>
        
            <v-card-actions>
              <v-btn
                color="orange lighten-2"
                text
              >
                Explore
              </v-btn>
        
              <v-spacer></v-spacer>
        
              <v-btn
                icon
                @click="show = !show"
              >
                <v-icon>{{ show ? 'mdi-chevron-up' : 'mdi-chevron-down' }}</v-icon>
              </v-btn>
            </v-card-actions>
        
            <v-expand-transition>
              <div v-show="show">
                <v-divider></v-divider>
        
                <v-card-text>
                  I'm a thing. But, like most politicians, he promised more than he could deliver. You won't have time for sleeping, soldier, not with all the bed making you'll be doing. Then we'll go with that data file! Hey, you add a one and two zeros to that or we walk! You're going to do his laundry? I've got to find a way to escape.
                </v-card-text>
              </div>
            </v-expand-transition>
          </v-card>
        </v-app>
      </div>
    </div>
  </div>

</template>

<script>
import axios from 'axios';

export default{
  data(){
    return {
      show: false,
      pokemons:[],
    };
  },
  created(){
    let instance = this;
    for(let i; i<=5 ; ++i){
      axios
        .get('https://pokeapi.co/api/v2/pokemon/${i+1}')
        .then((response) =>{
          let pokemon = {
            name: response.data.name,
            url: response.data.sprites.front_default,
          } 
          instance.pokemons.push(pokemon)
        })
        .catch ((err)=>{
          console.log(err);
        });
    }
    console.log(this.pokemons)
  }
};
</script>
<style scoped>
.logo{
  text-align: center;
  margin-top: 1%;
}
.mano{
  cursor: pointer;
}
</style>