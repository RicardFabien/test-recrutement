<template>
    <div :idTodo=idTodo>
        <p>Titre</p>
        <textarea v-on:change ="$emit('update:title',newTitle)"></textarea>
        <p>Description</p>
        <textarea v-model="description"></textarea>
        <p>{{date}}</p>
        <button v-on:click="$emit('removeCard',idTodo)">Supprimer</button>
    </div>
</template>

<script>
export default {
    name:"TodoCard",
    props:["idTodo","title","description","date"]
}
</script>