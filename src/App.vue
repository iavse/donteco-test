<template>
  <div id="app">
    <div v-if="mode === 'edit'" class="media-editor-container">
      <MediaEditor
        :playlist="playlist"
        v-on:add="addMedia"
        v-on:remove="deleteMedia"
        @play="mode = 'play'"/>
    </div>
    <div v-else-if="mode === 'play'" class="media-player-container">
      <MediaPlayer :playlist="playlist" @edit="mode = 'edit'"/>
    </div>
  </div>
</template>

<script>
import MediaEditor from './components/MediaEditor.vue';
import MediaPlayer from './components/MediaPlayer.vue';

export default {
  name: 'app',
  data: function () {
    return {
      playlist: [],
      mode: 'edit',
    }
  },
  components: {
    MediaEditor, MediaPlayer
  },
  computed: {
    currentView: () => ({play: MediaPlayer, edit: MediaEditor}[this.mode]),
  },
  methods: {
    nextId: (()=> {
      let id = 0
      return () => (id++)
    })(),
    addMedia: function(file) {
      const reader = new FileReader()
      reader.onload = (() => {
        const self = this
        const id = this.nextId()
        this.playlist.push({id, type: 'load', filename: '', dataUrl: ''})
        return function(e) {
          self.$set(self.playlist, self.playlist.findIndex((item) => (item.id === id)), {
            id,
            type: file.type,
            filename: file.name,
            dataUrl: e.target.result
          })
        }
      })()
      reader.readAsDataURL(file)
    },
    deleteMedia: function(id) {
      this.playlist.splice(this.playlist.findIndex((item) => (item.id === id)), 1)
    }
  }
}
</script>

<style>
#app {
  -webkit-box-sizing: border-box;
  -moz-box-sizing: border-box;
  box-sizing: border-box;
  width: 100%;
  height: 100%;
}
.media-editor-container, .media-player-container {
  -webkit-box-sizing: border-box;
  -moz-box-sizing: border-box;
  box-sizing: border-box;
  position: relative;
  width: 100%;
  height: 100%;
  padding: 5px;
}
</style>
