<template>
  <div class="media-content" @click="$emit('click')">
    <component v-if="mediaType" v-bind:is="mediaType" :filename="filename" :src="dataUrl"  :play="play"
      @start="$emit('start')" @ended="$emit('ended')"></component>
  </div>
</template>

<script>

import ImageMedia from './ImageMedia.vue';
import AudioMedia from './AudioMedia.vue';
import VideoMedia from './VideoMedia.vue';
import LoadMedia from './LoadMedia.vue';

const MEDIA_TYPES = {
  ImageMedia: ['image/jpeg', 'image/png'],
  AudioMedia: ['audio/mp3', 'audio/aac', 'audio/mpeg'],
  VideoMedia: ['video/mp4'],
  LoadMedia: ['load'],
}

export default {
  name: 'Media',
  props: {
    filename: String,
    type: String,
    dataUrl: String,
    play: Boolean,
  },
  computed: {
    mediaType: function() {
      for (const type in MEDIA_TYPES) {
        if (MEDIA_TYPES[type].indexOf(this.type) !== -1) {
          return type;
        }
      }
      return undefined;
    }
  },
  components: {
    ImageMedia, AudioMedia, VideoMedia, LoadMedia
  }
}
</script>


<style>
.playing {
  -webkit-box-shadow: 0 0 10px #444;
  box-shadow: 0 0 50px #148;
}
.paused {
  box-shadow: 0 0 50px #83e;
}
</style>
