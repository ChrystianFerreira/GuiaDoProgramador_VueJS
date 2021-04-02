<template>
  <div >
    <div id="pokemonCard">
      <div class="card-image">
        <figure >
          <img id="pokemonImage" @mouseup=trocarSprite :src="this.currentImg" alt="Placeholder image" />
        </figure>
      </div>
      <div class="card-content">
        <div class="media">
          <div class="media-content">
            <p class="title is-4">{{ name | upper }}</p>
            <p class="subtitle is-6">{{ this.pokemon.type }}</p>
          </div>
        </div>
        <div class="content"></div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  created: function () {
    axios.get(this.url).then((res) => {
      this.pokemon.type = res.data.types[0].type.name;
      this.pokemon.type = this.pokemon.type[0].toUpperCase() + this.pokemon.type.slice(1);
      this.pokemon.front = res.data.sprites.front_default;
      this.pokemon.back = res.data.sprites.back_default;
      this.currentImg = this.pokemon.front;
      console.log(this.pokemon);
    });
  },
  data() {
    return {
      currentImg: "",
      isFront: true,
      pokemon: {
        type: "",
        front: "",
        back: "",
      },
    };
  },
  props: {
    num: Number,
    name: String,
    url: String,
    type: String
  },
  filters: {
    upper: function (value) {
      var newName = value[0].toUpperCase() + value.slice(1);
      return newName;
    },
  },
  methods: {
    trocarSprite: function() {
      if(this.isFront){
        this.isFront = false;
        this.currentImg = this.pokemon.back
      } else {
        this.isFront = true;
        this.currentImg = this.pokemon.front;
      }
    },
  }
};
</script>
<style>
#pokemonCard{
  border-radius: 8px;
  min-width: 200px;
  min-height: 150px;
  background: rgb(251,255,152);
  background: radial-gradient(circle, rgba(251,255,152,1) 68%, rgba(252,255,122,1) 75%, rgba(253,228,84,1) 95%); 
  border-width: 7px;
  border-color: #FDE454;
}

#pokemonImage {
  margin-top: 25px;
  border-style: solid;
  border-width: 4px;
  border-color: #FDE454;
  border-radius: 5px;
  background: rgb(251,255,152);
  background: radial-gradient(circle, rgba(251,255,152,1) 68%, rgba(252,255,122,1) 75%, rgba(253,228,84,1) 95%);  
  box-shadow: 7px 3px 10px -2px #393938;
}
</style>