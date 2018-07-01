<template>
  <div  class="media-conent">
    <img :src="src"/>
  </div>
</template>

<script>
export default {
  name: 'ImageMedia',
  playing: null,
  props: {
    src: String,
    play: Boolean
  },
  watch: {
    play(value) {
      console.log('1')
      value ? this.start() : this.pause()
    }
  },
  methods: {
    start() {
      this.playing = setTimeout( () => {
        this.playing = null
        this.$emit('ended')
      }, 5000)
    },
    pause() {
      if (this.playing) {
        clearInterval(this.playing)
        this.playing = null
      }
    },
  },
  mounted() {
    if (this.play) {
      this.start()
    }
  },


}
</script>

<style scoped>
img {
  display: block;
  max-height: 180px;
  max-width: 240px;
}
</style>
