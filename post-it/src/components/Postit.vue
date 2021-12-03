<template>

<div class="postit">

    <h2>{{postitData.title}}</h2>

    <p v-for="text in postitData.content" v-bind:key="postitData.content.indexOf(text)" >
        {{text}}
    </p>
    <button class="button"><router-link :to="'/note/' + postitData._id">Details</router-link></button> 
    <button class="button"><router-link :to="'/edit/' + postitData._id">Edit</router-link></button>
    <button class="button" v-on:click="deleteById">X</button>
</div>
</template>

<script>



export default {
    name: "Postit",
    props: {
        postitData: null,
        id: {
            type: String,
            required: true,
            },
    },


    
    methods: {

    deleteById(){
            var axios = require('axios');
            var data = '';

            var config = {
            method: 'delete',
            url: 'http://5.135.119.239:3090/notes/' + this.id,
            headers: { },
            data : data
            };

            axios(config)
            .then(function (response) {
            console.log(JSON.stringify(response.data));
            })
            .catch(function (error) {
            console.log(error);
            });

        }
    },
    



};
</script>

<style scoped>
.postit{
    width: 400px;
    height: 300px;
    background-color: aqua;
    border-radius: 5%;
    overflow:hidden;


}
.button{
     font-size: 20px;
  font-weight: 200;
  letter-spacing: 1px;
  padding: 13px 50px 13px;
  outline: 0;
  border: 1px solid black;
  border-radius: 70%;
  
  cursor: pointer;
  position: relative;
  background-color: rgba(0, 0, 0, 0);
}
.btn{


padding:0.3em 1.2em;
border-radius:2em;
 float:bottom;
}
</style>