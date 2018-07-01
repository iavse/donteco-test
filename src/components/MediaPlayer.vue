<template>
  <div class="player">
      <div v-for="({id, filename, type, dataUrl}, index) in playlist" :key="id" class="media-container">
        <media :type="type" :filename="filename" :data-url="dataUrl"
        :play="isPlaying && current === index" :class="{playing: isPlaying && current === index, paused: current== index && !isPlaying}" @ended="next()" @click="play(index)"/>
      </div>
    <button class="edit-button" title="Edit" @click="$emit('edit')"></button>
    <div>
      <div v-if="playlist.length">
        <button class="play-button" title="Play" @click="play(current)"></button>
        <button class="pause-button" title="Pause" @click="pause()"></button>
        <button class="skip-button" title="Skip" @click="next()"></button>
      </div>
    </div>
  </div>
</template>

<script>
import Media from './Media.vue'

export default {
  name: 'MediaPlayer',
  data: function() {
    return {
      isPlaying: true,
      current: 0,
      last: 0,
    }
  },
  props: {
    playlist: Array
  },
  components: {
    Media
  },
  methods: {
    next() {
      this.current = this.current + 1 === this.playlist.length ?
                     0 :
                     this.current + 1
    },
    pause() { this.isPlaying = false },
    play(i) { this.isPlaying = true; this.current = i },
  }
}
</script>

<style scoped>
.player {
  padding: 20px;
  box-sizing: border-box;
  border-radius: 10px;
  width: 100%;
  height: 100%;
  overflow-y: auto;
  display: flex;
  flex-flow: column nowrap;
  align-items: center;
}
.media-container {
  position: relative;
  margin-bottom: 5px;
  /*width: 280px;*/
  max-width: 240px;
  max-height: 200px;
}
button {
  margin: 5px;
  outline: none;
  width: 50px;
  height: 50px;
  background-size: 50px;
  border: none;
  border-radius: 50%;
  box-shadow: 0 0 10px #222;
}
button:active {
  box-shadow: 0 0 0px #222;
}
.pause-button {
  background-image: url(../assets/pause.png);
}
.play-button {
  background-image: url(../assets/play.png);
}
.skip-button {
  background-image: url(../assets/skip.png);
}
.edit-button {
  background-image: url(data:image/svg+xml;utf8;base64,PD94bWwgdmVyc2lvbj0iMS4wIiBlbmNvZGluZz0iaXNvLTg4NTktMSI/Pgo8IS0tIEdlbmVyYXRvcjogQWRvYmUgSWxsdXN0cmF0b3IgMTkuMC4wLCBTVkcgRXhwb3J0IFBsdWctSW4gLiBTVkcgVmVyc2lvbjogNi4wMCBCdWlsZCAwKSAgLS0+CjxzdmcgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIiB4bWxuczp4bGluaz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94bGluayIgdmVyc2lvbj0iMS4xIiBpZD0iQ2FwYV8xIiB4PSIwcHgiIHk9IjBweCIgdmlld0JveD0iMCAwIDYwIDYwIiBzdHlsZT0iZW5hYmxlLWJhY2tncm91bmQ6bmV3IDAgMCA2MCA2MDsiIHhtbDpzcGFjZT0icHJlc2VydmUiIHdpZHRoPSI2NHB4IiBoZWlnaHQ9IjY0cHgiPgo8cGF0aCBkPSJNNDcsMTdjLTcuMTY4LDAtMTMsNS44MzItMTMsMTNjMCw0LjYzNCwyLjQ0NCw4LjY5OCw2LjEwNCwxMUgxOS44OTZDMjMuNTU2LDM4LjY5OCwyNiwzNC42MzQsMjYsMzBjMC03LjE2OC01LjgzMi0xMy0xMy0xMyAgUzAsMjIuODMyLDAsMzBzNS44MzIsMTMsMTMsMTNoMzRjNy4xNjgsMCwxMy01LjgzMiwxMy0xM1M1NC4xNjgsMTcsNDcsMTd6IE0yLDMwYzAtNi4wNjUsNC45MzUtMTEsMTEtMTFzMTEsNC45MzUsMTEsMTEgIHMtNC45MzUsMTEtMTEsMTFTMiwzNi4wNjUsMiwzMHogTTQ3LDQxYy02LjA2NSwwLTExLTQuOTM1LTExLTExczQuOTM1LTExLDExLTExczExLDQuOTM1LDExLDExUzUzLjA2NSw0MSw0Nyw0MXoiIGZpbGw9IiMwMDZERjAiLz4KPGc+CjwvZz4KPGc+CjwvZz4KPGc+CjwvZz4KPGc+CjwvZz4KPGc+CjwvZz4KPGc+CjwvZz4KPGc+CjwvZz4KPGc+CjwvZz4KPGc+CjwvZz4KPGc+CjwvZz4KPGc+CjwvZz4KPGc+CjwvZz4KPGc+CjwvZz4KPGc+CjwvZz4KPGc+CjwvZz4KPC9zdmc+Cg==);
}
</style>
