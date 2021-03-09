<template>
    <div :idTodo=idTodo>
        
        <v-row>
            <v-col
                cols="12"
                sm="6"
                md="4"
            >
                <v-text-field label="Title" v-model="title" 
                v-on:change ="$emit('changeTitle',title)"></v-text-field>

                <p>{{date}}</p>
            </v-col> 

            <v-col
                col = "12"
                sm = "6"
                md = "4"
            >
                <v-textarea label="Description" outlined v-model="description" 
                v-on:change ="$emit('changeDesc',description)"></v-textarea>
            </v-col>

            <v-col
                col = "12"
                sm = "6"
                md = "2"
            >
                <v-btn style="background-color: rgb(212, 60, 0); border-color: rgb(212, 60, 0);" 
                v-on:click="$emit('removeCard',idTodo)">Supprimer</v-btn>

            </v-col>

        </v-row>
    </div>
</template>

<script>
export default {
    name:"TodoCard",
    props:["idTodo","title","description","date"]
}
</script>