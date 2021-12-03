<template>
  <div  class="home">
    <ModalForm v-if="showModal" />
    
    <h1>POSTITS</h1>
    <input type="text" v-model="search" placeholder="search by title"/><br>
    <div v-for="item in filteredlist" v-bind:key= "item._id" class="for" >
      <Postit :postitData="item" :id="item._id"/>
    </div>
    <div class= "container" id="app">
    

    <button type="button" class="btn btn-info" v-on:click="toggleModal">create new post-it</button>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import Postit from "@/components/Postit";
import ModalForm from "@/components/ModalForm";

var axios = require('axios');

export default {
  name: "Home",
  components: {  
    Postit,
    ModalForm,

  },
  
    data() {
        return {
            list: [],
            showModal: false,
            search:''
        }
  },
    methods: {
    toggleModal (){
      
      this.showModal =! this.showModal;
    }
  },
computed:{
  filteredlist: function(){
    return this.list.filter((item) => {
      return item.title.toLowerCase().match(this.search.toLowerCase());
    });
  }
},
  
    mounted() {
        var config = {
        method: 'get',
        url: 'http://5.135.119.239:3090/notes',
        headers: { }
        };

        axios(config)
        .then((response) => {
            console.log("list");
          this.list = [...response.data.notes];


        })
        .catch(function (error) {
        console.log(error);
        });
    },




}
</script>
<style scoped>

.for{
  display: inline-flex;
  margin: 5px;
}
.btn{
    position: fixed;
      bottom: 200px;
      right: 200px; 
      padding:0.3em 1.2em;
    border-radius:2em;
}
</style>