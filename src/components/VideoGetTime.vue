<template>
    <div class="ml-auto pr-8">
        <p>{{ videoTime }} seconds</p>
        <video class="hideVideo" ref="videoRef">
            <source :src=videoItem.link type="video/mp4">
            Your browser does not support the video tag.
        </video>
    </div>
</template>

<script>
export default {
    props: [
        'videoItem',
    ],
    data() {
        return {
            videoFile: null,
            videoTime: null,
        }
    },
    mounted: function () {
        this.videoFile = this.$refs.videoRef
        this.videoFile.onloadedmetadata = (event) => {
            this.videoTime = Math.round(this.videoFile.duration * 100) / 100
        };
    },
}
</script>
<style>
.hideVideo {
    display: none;
}
</style>