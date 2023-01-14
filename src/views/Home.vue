<template>
  <div class="mx-auto max-w-lg">
    <div class="divide-y divide-gray-100">
      <div v-for="videoItem in video" :key="videoItem.id">
        <div class="group py-4" v-bind:class="{ active: this.openId === videoItem.id }">
          <div @click="showVideo(videoItem)"
            class="flex cursor-pointer list-none items-center justify-between text-lg font-medium text-secondary-900">
            {{ videoItem.name }}
            <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5"
              stroke="currentColor" class="block h-5 w-5 transition-all duration-300">
              <path stroke-linecap="round" stroke-linejoin="round" d="M19.5 8.25l-7.5 7.5-7.5-7.5" />
            </svg>
          </div>
          <div class="mt-2 text-secondary-500">
            <VideoSingle :videoItem="videoItem" v-if="videoItem.id === this.openId" />
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import VideoList from "../data/VideoList.json";
import VideoSingle from "../components/VideoSingle.vue"
export default {
  data() {
    return {
      video: VideoList,
      openId: null,
    };
  },
  components: {
    VideoSingle
  },
  methods: {
    showVideo(videoItem) {
      if (this.openId === videoItem.id) {
        this.openId = false
      }
      else (
        this.openId = videoItem.id
      )
    }
  }
};
</script>

<style>
.group.active svg {
  transform: rotate(180deg);
}
</style>