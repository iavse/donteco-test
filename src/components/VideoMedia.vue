<template>
  <div>
    <p class="title">{{filename}}</p>
    <video ref="elem" :src="src" controls @ended="handleEnded()" ></video>
  </div>
</template>

<script>
export default {
  name: 'VideoMedia',
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
  methods: {
    handleEnded() {
      this.$emit('ended')
    }
  }
}
</script>

<style scoped>
p {
  display: block;
  text-align: center;
  margin: 0;
  padding: 5px;
}
video {
  display: block;
  max-width: 100%;
  max-height: 100%;
}
</style>
