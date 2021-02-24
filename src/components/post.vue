<template>
    <div id ="post">
        <p>{{post.content}}</p>
        <button @click="update = true " > Edit </button>"
        <button @click="deletePost(post.id)" :disabled = delete_disable> Delete </button>
        <div v-if="update">
            <textarea v-model="content" name="" cols="30" rows="10"></textarea>
            <button @click="updatePost(post.id)" :disabled= update_disable> Update </button>
        </div>

    </div>
</template>

<script>
import axios from "axios"

    export default {
        name:"post-component",
        props: {
            post: {
                type: Object,
                required: true 
            },
        },
        mounted () {
            this.content= this.post.content;
        },
        data() {
            return {
                id:"",
                content: "",
                update: false,
                update_disable:false,
                delete_disable:false
            }
        },
        methods: {
            updatePost(id) {
                this.update_disable=true
                axios.request({
                    url: "http://127.0.0.1:5000/api/posts", 
                    method: "PATCH",
                    data: {
                        "id":id,
                        "content":this.content
                    }
                    
                }).then((res)=>{
                    this.update = false
                    this.post.content = res.data.content;
                    this.update_disable =false
                }).catch((err)=>{
                    console.log(err);
                    this.update_disable=false;
                })
            },
            deletePost(id){
                this.delete_disable=true
                axios.request({
                    url: "http://127.0.0.1:5000/api/posts", 
                    method: "DELETE",
                    data:{
                        "id":id,
                        "content":this.content
                    }
                
                }).then(()=>{
                    this.delete_disable =false
                    location.reload();
                }).catch((err)=>{
                    console.log(err);
                    this.delete_disable= false;
                })

                
            }
        },

    }
</script>

<style scoped>
#post{
    width: 50%;
    border-bottom: 2px solid gray ;
    margin-left: 25%;
}

</style>