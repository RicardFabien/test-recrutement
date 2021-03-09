<template>
  <div>
    <v-btn @click ="addCard">Add</v-btn>
    <hr/>
    <div v-for="card in cards" :key="card.id">
        <div :idTodo=card.id>
        
        <v-row>
            <v-col
                cols="12"
                sm="6"
                md="4"
            >
                <v-text-field label="Title" v-model="card.title" 
                v-on:change ="changeTitle(card.id,card.title)"></v-text-field>

                <p>{{card.date}}</p>
            </v-col> 

            <v-col
                col = "12"
                sm = "6"
                md = "4"
            >
                <v-textarea label="Description" outlined v-model="card.description" 
                v-on:change ="changeDescription(card.id,card.description)"></v-textarea>
            </v-col>

            <v-col
                col = "12"
                sm = "6"
                md = "2"
            >
                <v-btn style="background-color: rgb(212, 60, 0); border-color: rgb(212, 60, 0);" 
                v-on:click="removeCard(card.id)">Supprimer</v-btn>

            </v-col>

        </v-row>
    </div>
    </div>
  </div>
</template>

<script lang="ts">
import Vue from "vue";

interface Card{
  id:number,
  title : string,
  description: string,
  date : string

}

interface cardData{
  cards : Array<Card>
}

var data:cardData;

export default Vue.extend({
  components:{
  },
  data() {
    var storage = window.localStorage;
    let toParse : string | null = storage.getItem("cards");
    let treated : string= (toParse === null)?"":toParse;
    var cards : Array<Card> | null = JSON.parse(treated);
    if (cards === null) 
      cards = [];
    return {
      cards : cards
    }
      
  },
  methods:{
    addCard(): void{

        let newCard : Card = {
          id:this.cards.length === 0?0:this.cards[this.cards.length-1].id+1,
          title:"",
          description:"",
          date: new Date().toString()
        }

        this.cards.push(newCard);
        this.modifyCards();;
    },

    removeCard(idTodo : number): void{
      let card:Card|undefined = this.getCardById(idTodo);

      if (card !== undefined){
        this.cards.splice(
          this.cards.indexOf(
            card
          ), 1
        );
        this.modifyCards();
      }
        
    },

    modifyCards(): void{
      localStorage.setItem("cards",JSON.stringify(this.cards));
    },
    changeTitle(idTodo : number,title :string): void{
      let card : Card|undefined = this.getCardById(idTodo);
      if (card !== undefined){
        card.title = title;

        this.changeCard(idTodo)
      }
      
    }
    ,
    changeDescription(idTodo: number,description: string): void{
      let card : Card|undefined = this.getCardById(idTodo);
      if (card !== undefined){
        card.description = description;

        this.changeCard(idTodo)
      }
    },

    changeCard(idTodo: number): void{
      let card : Card|undefined = this.getCardById(idTodo);
      if (card !== undefined){
        card.date = new Date().toString();

        this.modifyCards();
      }
    },

    getCardById(idTodo : number): Card|undefined {
      let card  : Card|undefined = this.cards.find((elem:Card) => elem.id === idTodo );
      return card;
    }
  }
})
</script>
