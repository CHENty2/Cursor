<template>
  <div>
    <h2 :style="{ color: rgbColor }">陈天阳，我的神！</h2>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data() {
    return {
      r: 255,
      g: 0,
      b: 0,
      animationId: null
    }
  },
  computed: {
    rgbColor() {
      return `rgb(${this.r}, ${this.g}, ${this.b})`
    }
  },
  mounted() {
    let phase = 0
    const step = () => {
      phase = (phase + 1) % 360
      const rad = (phase * Math.PI) / 180
      this.r = Math.round((Math.sin(rad) * 127) + 128)
      this.g = Math.round((Math.sin(rad + (2 * Math.PI) / 3) * 127) + 128)
      this.b = Math.round((Math.sin(rad + (4 * Math.PI) / 3) * 127) + 128)
      this.animationId = requestAnimationFrame(step)
    }
    this.animationId = requestAnimationFrame(step)
  },
  beforeUnmount() {
    cancelAnimationFrame(this.animationId)
  }
}
</script>

<style scoped>
h2 {
  font-size: 2rem;
  transition: color 0.01s;
}
</style>

