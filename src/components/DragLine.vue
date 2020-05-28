<template>
  <div
    ref="line"
    class="middle-drag-line"
    draggable="false"
    :class="{'is-horizontal': isHorizon, 'is-vertical': !isHorizon}"
    :style="lineStyle"
    @click.stop.prevent
    @mousedown.stop.prevent="handleMouseDown"
  >

  </div>
</template>
<script>
export default {
  props: {
    isHorizon: {
      type: Boolean,
      default: true
    },
    lineColor: {
      type: String,
      default: '#F7F8FA'
    },
    lineLength: {
      type: [Number, String],
      default: 12
    },
    transformKey: {
      type: String,
      default: 'flex-basis'
    },
    max: {
      type: Number,
      default: 600
    },
    min: {
      type: Number,
      default: 200
    }
  },
  data() {
    return {
      preLength: 0,
      parentEl: null,
      preEl: null
    }
  },
  computed: {
    lineStyle() {
      const _style = {}
      const _lengthKey = this.isHorizon ? 'height' : 'width'
      if (typeof this.lineLength == 'number') {
        _style[_lengthKey] = `${this.lineLength}px`
      } else if (typeof this.lineLength == 'string') {
        _style[_lengthKey] = this.lineLength
      }
      _style.backgroundColor = this.lineColor
      return _style
    }
  },
  mounted() {
    this.preEl = this.$refs.line.previousElementSibling
    this.parentEl = this.$refs.line.parentElement
    this.preLength = parseInt(getComputedStyle(this.preEl)[this.transformKey])
  },
  methods: {
    handleMouseDown(e) {
      this.parentEl.addEventListener('mousemove', this.handleMouseMove)
      this.parentEl.addEventListener('mouseup', this.removeEvent)
      this.parentEl.addEventListener('mouseleave', this.removeEvent)
    },
    handleMouseMove(e) {
      this.preLength += this.isHorizon ? e.movementY : e.movementX
      this.preLength = Math.max(this.min, this.preLength)
      this.preLength = Math.min(this.max, this.preLength)
      this.preEl.style[this.transformKey] = `${this.preLength}px`
    },
    removeEvent(e) {
      this.parentEl.removeEventListener('mousemove', this.handleMouseMove)
      this.parentEl.removeEventListener('mouseup', this.handleMouseUp)
      this.parentEl.removeEventListener('mouseleave', this.handleMouseLeave)
    }
  }
}
</script>
<style>
.middle-drag-line {
  display: flex;
  align-items: center;
  justify-content: center;
}
.is-horizontal {
  cursor: n-resize;
  width: 100%;
}
.is-vertical {
  cursor: col-resize;
  height: 100vh;
}
</style>