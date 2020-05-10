<template>
  <div id="app">
    <h1>Match Cards Game</h1>
    <h3>Instruction:</h3>
    <p>Click on one card to flip it. Once you have found a matching pair click the Check Match button. </p>
      <p>Clicks counter: {{clicks}}</p>
      <h2 v-show="end">You won in {{clicks}} clicks</h2>
    <main>
      <div v-show="!card.matched" id="card" v-on:click='clicks++;card.up = !card.up' v-for="card in cards" v-bind:class="{card:!card.up, up:card.up}">
        <img v-if='card.up' v-bind:src="card.path" alt="a card">
      </div>
    </main>
    <button type="button" name="button" v-on:click='restart()'>Restart</button>
    <button type="button" name="button" v-on:click='match();ended()'>Check Match</button>
  </div>
</template>

<script>
export default {
  data () {
    return {
      cards: [],
      clicks: 0,
      matches: 0,
      end: false
    }
  },
  methods:{
    match:function(){
      let card ="";
      for(let key in this.cards){
        if (this.cards[key].up && !this.cards[key].matched) {
          if (card == "") {
              card = this.cards[key]
              console.log("First true card");
              console.log(card);
          }else{
              if (card.path == this.cards[key].path) {
                this.matches += 1;
                card.matched = true;
                console.log("Changing card matched to true" + card.matched);
                this.cards[key].matched =true;
                console.log(this.matches);
              break;
            }
          }
        }
      }
    },
    ended:function(){
      if (this.matches == 4) {
        this.end = true;
      }
    },
    restart:function(){
      for(let key in this.cards){
        this.cards[key].up = false;
        this.cards[key].matched = false;
      }
      this.end = false;
      this.clicks = 0;
      this.matches = 0;
    }
  },
  created(){
    let numArray =[1,2,3,4,1,2,3,4];
    let card;
    var j,temp;
    for (var i = 7 ; i > 0 ; i--) {
      j = Math.floor(Math.random() * (i + 1));
      temp = numArray[i];
      numArray[i] = numArray[j];
      numArray[j] = temp;
    }
    for (let key in numArray){
      card = {
        path:'src/assets/card'+ numArray[key] +'.png', up:false, matched:false
      }
      this.cards.push(card);
    }
    console.log(numArray);
    console.log(this.cards);
  }
}
</script>

<style>
#app{
  width: 90%;
  margin: auto;
  text-align: center;
}
h1{
  color: #9b3c2e;
}
main{
  display: grid;
  grid-template-columns: auto auto auto;
  grid-row-gap: 40px;

}
#card{
  width: 278px;
  height: 386px;
  margin: auto;
}
.card{
  background-color: #dde0b6;
  border: 1px solid #dde0b6;
  text-align: center;
}
.up{
  background-color: none;
}
button{
  margin: 2%;
  padding: 2%;
  font-size: 24px;
  color: #9b3c2e;
  background-color: #f3e6be;
  border: 1px solid #f3e6be;
}
img{
  width: 100%;
}
</style>
