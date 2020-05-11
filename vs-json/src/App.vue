<template>
  <div id="app">
<h1>Digimon Adventure </h1>
<div id="frame">

<div class="slides" for v-for="slide in info" v-bind:id="slide.id" v-bind:class="isActive(slide.id)">
  <div class="text">
    <h3>Name: {{slide.name}}</h3>
    <p class="description">Description: {{slide.description}}</p>
    <p class="digimon">Digimon: {{slide.digimon}}</p>
  </div>
  <div class="image">
 <img v-bind:src="slide.img" v-bind:alt="slide.name">
  </div>
</div>
  <button type="button" name="button" v-on:click='number--,checNumber()'>&#10094;</button>
  <button type="button" name="button" class="right" v-on:click="number++,checNumber()">&#10095;</button>
  </div>
<add-footer> </add-footer>
</div>
</template>

<script>
import axios from 'axios';
import Footer from './components/footer.vue';

export default {
  components: {
    'add-footer': Footer
  },
  data () {
    return {
      info:[],
      number: 0,
    }
  },
  methods:{
    isActive: function(id){
      return{
        active: id != this.number,
      }
    },
    checNumber: function(){
      console.log(this.number);
      console.log(this.info.length);
      if (this.number < 0) {
        this.number = this.info.length - 1;
      }else if( this.number > this.info.length - 1){
        this.number = 0;
      }
    }
  },
  created(){
    axios.get('src/' + 'info.json').then(data => {
      this.info = data.data;
    })
    }
  }
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Ubuntu&display=swap');

#app{
  padding: 2%;
  margin: auto;
  width: 80%;
  font-family: 'Ubuntu', sans-serif;
}
#frame{

    position: relative;
}
.slides{
  background-color:  #E27D60;
  display: grid;
  grid-template-columns: 50% auto;
  box-shadow: 5px 10px #41B3A3;

}
.slides .text{
  background-color: #E8A87C;
  line-height: 1.6;
  padding: 2%;
  display: grid;
  grid-template-rows: 10% 60% 10% ;
}

.slides .image{
    margin: auto;
}

.image img{
  width: 178px;
  height: 400px;
}
button{
  width: 40px;
  padding: 2%;
  background-color: #E8A87C;
  color: black;
  transition: 0.6s ease;
  border: none;
  position: absolute;
  top: 40%;
}
.right{
  right: 0;
  background-color:  #E27D60;
}
.active{
  display: none;
}
button:hover{
  background-color: #41B3A3;
  color: white;
}
</style>
