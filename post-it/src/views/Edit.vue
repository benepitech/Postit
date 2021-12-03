<template>
    <div class="modal">
      <h1>Create Post-it</h1>
        <div >
            <form class="modal-background">
                <input v-model="title" placeholder="title" />
                <input v-model="content" placeholder="content" />
         <button v-on:click="submit"></button>
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
                props: {
                id: {
                    type: String,
                    required: true,
                    },
            },
            
                methods: {
                    submit() {               
                
                        var data = JSON.stringify({
                            "title": this.title,
                            "content": this.content 
                        });

                        var config = {
                            method: 'put',
                            url: `http://5.135.119.239:3090/notes/${this.id}`, 
                            headers: { 
                                'Content-Type': 'application/json'
                            },
                            data : data
                            
                        };

                        axios(config)                        
                        .then(function (response) {
                            alert('this time it worked');
                            console.log(JSON.stringify(response.data));                        
                        })
                        .catch(function (error) {
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