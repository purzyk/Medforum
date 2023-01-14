<template>
    <div>
        <video class="video" ref="videoRef">
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

        }
    },

    mounted: function () {
        var videoFile = this.$refs.videoRef
        videoFile.play()
        console.log('start')
        videoFile.onloadedmetadata = function () {
            var delta = 0.05;
            setInterval(function () {
                if (videoFile.currentTime >= videoFile.duration * (0.5 - delta)
                    && videoFile.currentTime <= videoFile.duration * (0.5 + delta)) {
                    console.log('middle')
                }
            }, 1000);
        };
        videoFile.onended = function (e) {
            console.log('end')
        };
    },

}
</script>