<template>
  <div class="media-editor">
    <draggable :list="playlist" :options="{animation: 150}">
      <div v-for="{id, type, filename, dataUrl} in playlist" :key="id" class="media-container">
        <media :type="type" :filename="filename" :data-url="dataUrl"/>
        <button v-on:click="$emit('remove', id)">x</button>
      </div>
    </draggable>
    <label>
      <input type="file" v-on:change="handleChange"/>+
    </label>
    <button class="play-button" @click="$emit('play')"></button>
  </div>
</template>


<script>
import draggable from 'vuedraggable'
import Media from './Media.vue'


export default {
  name: 'MediaEditor',
  props: {
    playlist: Array
  },
  components: {
    Media, draggable
  },
  methods: {
    handleChange: function(e) {
      this.$emit('add', e.target.files[0])
      e.target.value = ''
    }
  },
}
</script>


<style scoped>
.play-button {
  margin-top: 8px;
  border: none;
  border-radius: 50%;
  width: 50px;
  height: 50px;
  display: -webkit-flex;
  display: -moz-flex;
  display: -ms-flex;
  display: -o-flex;
  display: flex;
  justify-content: center;
  -ms-align-items: center;
  align-items: center;
  font-size: 1.5em;
  padding: 0;
  -webkit-background-size: 50px;
  background-size: 50px;
  box-shadow: 0 0 10px #222;
  outline: none;
  background-image: url(../assets/play.png);
}
.play-button:active {
  box-shadow: 0 0 2px #222;
}
.media-editor {
  box-sizing: border-box;
  border-radius: 10px;
  width: 100%;
  height: 100%;
  overflow-y: auto;
  display: flex;
  flex-flow: column nowrap;
  align-items: center;
}
.media-container button {
  box-sizing: border-box;
  position: absolute;
  right: 0px;
  top: 0px;
  width: 1.5em;
  height: 1.5em;
  padding: 0;
  border: none;
  background-color: #fff;
  border-radius: 50%;
  line-height: 1.5em;
  background-color: rgba(255, 255, 255, 0.2);

}
.media-container {
  position: relative;
  margin-bottom: 5px;
  max-width: 280px;
  max-height: 200px;
}
.media-container button:hover {
  background-color: #fff;
}
label input {
  display: none;
}
label {
  display: flex;
  width: 50px;
  height: 50px;
  border: none;
  border-radius: 50%;
  justify-content: center;
  align-items: center;
  background-color: #ccc;
  font-size: 2em;
  font-weight: bold;
  color: #38c;
}
label:hover {
  background-color: #38c;
  color: #ccc;
}
label:active {
  background-color: #159;
}
</style>
