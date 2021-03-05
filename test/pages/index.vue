<template>
  <div>
    <button @click ="addCard">Add</button>
    <hr/>
    <todo-card v-for="card in cards" :key="card.id" v-bind:idTodo.sync="card.idTodo" 
    v-bind:title.sync="card.title" v-bind:description.sync="card.description" 
    v-bind:date.sync="card.date" v-on:removeCard="removeCard"/>


    
  </div>
</template>

<script>
import TodoCard from '../components/TodoCard.vue';

export default{
  components:{
    TodoCard
  },
  data(){
    console.log("IT'S ALIVE !");
    return {
      cards : [
        {idTodo:0,title:"titreTest",description:"Description test", date: "Date test"}
      ]
    }
      
  },
  methods:{
    addCard(){
        this.cards.push({
        id:this.cards.length === 0?0:this.cards[this.cards.length-1].id+1,
        title:"",
        description:"",
        date: Date.now()
        })
    },
    removeCard(idTodo){
      this.cards.splice(
        this.cards.indexOf(
          this.cards.find(elem => elem.id === idTodo )
        ), 1
      )
    },
    changeTitle(title){
      console.log(title);
    }
  }
}





</script>
