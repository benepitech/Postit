<template>
    <div class="modal">
      <h1>Create Post-it</h1>
        <div class="modal-background">
            <form >
                <input v-model="title" placeholder="title" />
                <input v-model="content" placeholder="content" />
         <button v-on:click="push"></button>
            </form>

        </div>
        
    </div>
</template>



<script>
var axios = require('axios');
    
export default {
    name: 'ModalForm',
        data(){
            return{
                
                title: '',
                content: '',
                
            }
        },
      
    methods: {
        push() {
      
      
   
            var data = {
                "title": this.title,
                "content": [this.content]
            };

            var config = {
                method: 'post',
                url: 'http://5.135.119.239:3090/notes',
                headers: { 
                    'Content-Type': 'application/json'
                },
                data : data
            };

            axios(config)
            .then(function (response) {
            console.log(JSON.stringify(response.data));
            })
            .catch(function (error) {
                alert();
            console.log(error);
            });

        }
    }
}
</script>

<style>


.modal-background{

    position: center;
    width: 300px;
    height: 200px;
    background-color: aqua;
    border-radius: 5%;
    overflow:hidden;
}
</style>