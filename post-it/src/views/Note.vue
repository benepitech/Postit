<template>

    <div> 
         <div v-for="item in list" v-bind:key= "item._id" class="for" >
      <Postit :postitData="item" />
    </div>
         <router-view />
    </div>
     
    
      

</template>
<script>

import Postit from "@/components/Postit";

var axios = require('axios');

export default {
  name: "Home",
  components: {  
    Postit,
   

  },
  
  
    data() {
        return {
            list: {},
            showModal: false,


        }
  },
  props: {
 id: {
  type: String,
  required: true,
 },
},
    methods: {
    toggleModal (){
      
      this.showModal =! this.showModal;
    }
  },

  
    mounted() {
      console.log(this.id);
        var config = {
        method: 'get',
        url: `http://5.135.119.239:3090/notes/${this.id}`, 
        headers: { }
        };

        axios(config)
        .then((response) => {
          
          this.list = response.data;

        console.log(response.data);

        })
        .catch(function (error) {
        console.log(error);
        });
    },




}

</script>


