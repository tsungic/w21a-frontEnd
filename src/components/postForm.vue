<template>
    <div>
        <h4>Write your post! </h4>
        <button @click="sendPost">submit </button>
        <textarea v-model="content" name="" id="" cols="30" rows="10"></textarea>
    </div>
</template>

<script>
import axios from "axios"
    export default {
        name: "postForm", 
        data() {
            return {
                content: "",
                disable:false,
            }
        },
        methods: {
            sendPost() {
                this.disable=true;
                axios.request({
            url: "http://127.0.0.1:5000/api/posts", 
            method: "POST",
            data: {content:this.content}
            }).then(()=>{console.log("Success")}).catch((err)=>{console.log(err)})
            }
        },
    }
</script>

<style scoped>

</style>