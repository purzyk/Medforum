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
            videoFile: null,
            intervalId: null,
            isPlaying: false,

        }
    },
    watch: {
        isPlaying(isPlaying) {
            if (this.intervalId !== null) {
                clearInterval(this.intervalId);
            }
            if (isPlaying) {
                const delta = 0.05;
                this.intervalId = setInterval(() => {
                    if (this.videoFile.currentTime >= this.videoFile.duration * (0.5 - delta)
                        && this.videoFile.currentTime <= this.videoFile.duration * (0.5 + delta)) {
                        console.log('middle')
                    }
                }, 1000);
            }
        }
    },
    mounted: function () {
        this.videoFile = this.$refs.videoRef
        this.videoFile.play()
        this.isPlaying = true;
        console.log('start')
        this.videoFile.onended = function () {
            console.log('end')
            this.isPlaying = false;
        };
    },
    beforeUnmount: function () {
        clearInterval(this.intervalId);
        this.isPlaying = false;
    },

}
</script>