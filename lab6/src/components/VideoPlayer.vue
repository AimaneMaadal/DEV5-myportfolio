<script setup>

import { onMounted, reactive, ref } from 'vue'
import 'animate.css';

    let src = ref('');
    let videos = reactive({ videos: [] });
    let animation = ref('animate__fadeIn');

    onMounted(() => {
        let api_url = "tiktok.json";
        fetch(api_url)
            .then(response => response.json())
            .then(data => {
                videos.videos = data.data.videos;
                src.value = videos.videos[0].video;
            }) 
    });

    let index = ref(0);

    const nextvideo = () => {
        index.value++;
        animation.value = 'animate__fadeOut';
        setTimeout(() => {
            animation.value = 'animate__fadeIn';
        }, 500);
        src.value = videos.videos[index.value].video;
    }

</script>

<template>
  <div>
    <div class="videoplayer">
        <div class="controls">
            <a @click="nextvideo" href="#" class="controls__next">➜</a>
        </div>
        <video :class="animation" class="animate__animated" id="video" controls autoplay :src="src" muted>
        </video>
    </div>
  </div>
</template>

<style scoped>
.controls{
    position: absolute;
    right: 5%;
    top: 50%;
    font-size: 10vw;
    z-index: 2;

}
.controls a{
    color: white !important;
    text-decoration: none !important;
}
#video{
    width: 100%;
    height: 100%;
}
.videoplayer{
    position: relative;
}
</style>
