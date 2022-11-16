<script setup>
import { onMounted, reactive, ref } from 'vue';



let VideoComments = reactive({ comments: [] });
let comment = ref('');

onMounted(() =>{
    const api_url = "https://lab5-p379.onrender.com/api/v1/messages";
    fetch(api_url)
        .then(response => response.json())
        .then(data => {
            VideoComments.comments = data;
            console.log(VideoComments.comments);
        })  
})



    const addComment = () => { 
        const api_url = "https://lab5-p379.onrender.com/api/v1/messages";
        fetch(api_url, {
            method: 'POST',
            headers: {
                'Content-Type': 'application/json'
            },
            body: JSON.stringify({
                user : "Aimane",
                text: comment.value
            })
        })
        //add comment to VideoComments reactive object
        VideoComments.comments.push({
            user: "Aimane",
            text: comment.value
        })
        
    }


</script>

<template>
  <div class="video_details">
    <h3>Comments</h3>
    <div v-for="comment in VideoComments.comments" :key="comment.id">
        <p><b>{{comment.user}}</b></p>
        <p>{{comment.text}}</p>
    </div>
    <input type="text" id="message" v-model="comment">
    <button @click="addComment">Add Comment</button>
  </div>
</template>

<style scoped>
.video_details{
  padding: 1rem;
}

</style>
