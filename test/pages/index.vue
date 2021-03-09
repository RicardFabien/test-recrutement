<template>
  <div>
    <v-btn @click ="addCard">Add</v-btn>
    <hr/>
    <todo-card v-for="card in cards" :key="card.id" v-bind:idTodo="card.idTodo"
    v-bind:title.sync="card.title" v-bind:description.sync="card.description" 
    v-bind:date.sync="card.date" v-on:removeCard="removeCard" 
    v-on:changeDesc="changeDescription(card.id, $event)" v-on:changeTitle="changeTitle(card.id,$event)"/>
  </div>
</template>

<script lang="ts">
import TodoCard from '../components/TodoCard.vue';

interface Card{
  id:number,
  title : string,
  description: string,
  date : string

}

export default{
  components:{
    TodoCard
  },
  data(){
    var storage = window.localStorage;
    var cards : Array<Card> | null = JSON.parse(storage.getItem("cards"));
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
      this.cards.splice(
        this.cards.indexOf(
          this.cards.find(elem => elem.id === idTodo )
        ), 1
      );
      this.modifyCards();
    },

    modifyCards(): void{
      localStorage.setItem("cards",JSON.stringify(this.cards));
    },
    changeTitle(idTodo : number,title :string): void{
      let card : Card = this.cards.find(elem => elem.id === idTodo );
      card.title = title;

      this.changeCard(idTodo)
    }
    ,
    changeDescription(idTodo: number,description: string): void{
      let card : Card = this.cards.find(elem => elem.id === idTodo );
      card.description = description;

      this.changeCard(idTodo)
    },

    changeCard(idTodo: number): void{
      let card : Card = this.cards.find(elem => elem.id === idTodo );
      card.date = new Date().toString();

      this.modifyCards(idTodo);

    }
  }
}
</script>
