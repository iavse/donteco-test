<template>
  <div>
    <p>{{filename}}</p>
    <audio ref="elem" controls :src="src" @ended="$emit('ended')"></audio>
  </div>
</template>

<script>
export default {
  name: 'AudioMedia',
  data: function() {
    return {
      playing: false
    }
  },
  props: {
    filename: String,
    src: String,
    play: Boolean
  },
  watch: {
    play(value) {
      value ? this.$refs.elem.play() : this.$refs.elem.pause()
    }
  },
  mounted() {
    this.play && this.$refs.elem.play()
  },
}
</script>

<style scoped>
p {
  margin-top: 0;
  margin-bottom: 5px;
}
audio {
  max-width: 100%;
  max-height: 100%;
}
</style>
