<script setup>
import { onMounted, ref } from 'vue';


let Username = ref('');
let Description = ref('');

onMounted(() =>{
    const api_url = "tiktok.json";
    fetch(api_url)
        .then(response => response.json())
        .then(data => {
            Username.value = data.data.videos[0].username;
            Description.value = data.data.videos[0].description;
        })  
})




</script>

<template>
  <div class="video_details">
    <h3>{{Username}}</h3>
    <p>{{Description}}</p>
  </div>
</template>

<style scoped>
.video_details{
  padding: 1rem;
}

</style>
