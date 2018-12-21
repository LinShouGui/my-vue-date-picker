<template>
  <div class="my-color-picker" :style="{background:color,width:pickWidth+'px',height:pickHeight+'px'}" @click.stop="show=!show">
    <div v-if="isShowText" class="pick" :style="{height:pickHeight+'px',lineHeight:pickHeight+'px',pointerEvents:isClickEqualPick?'auto':'none'}">
      {{color}}
    </div>
    <div v-show="show" class="pickArea" :style="{left:(-width / 2 + pickWidth / 2) + 'px', width:width+'px',height:height+'px'}">
      <canvas id="colorPicker" @mousemove="hdleMove" @click.stop="hdleClick"></canvas>
    </div>
  </div>
</template>

<script>
export default {
  name: 'MyColorPicker',
  props: {
    isShowText: {
      type: Boolean,
      default: true
    },
    isClickEqualPick: {
      type: Boolean,
      default: false
    },
    pickWidth: {
      type: Number,
      default: 20
    },
    pickHeight: {
      type: Number,
      default: 20
    },
    width: {
      type: Number,
      default: 200
    },
    height: {
      type: Number,
      default: 200
    },
    colors: {
      type: Array,
      default: () => ['red', 'orange', 'yellow', 'green', 'blue', 'indigo', 'violet']
    },
    italic: {
      type: Boolean,
      default: false
    },
    vertical: {
      type: Boolean,
      default: false
    },
    ritalic: {
      type: Boolean,
      default: true
    }
  },
  data () {
    return {
      color: '#000',
      ctx: null,
      show: false
    }
  },
  computed: {
    len () {
      return this.colors.length
    }
  },
  mounted () {
    let canvas = document.querySelector('.my-color-picker #colorPicker')
    let {
      width,
      height,
      len
    } = this
    let myGradient
    if (!canvas) throw new Error('未找到挂载colopicker的dom: .my-color-picker #colorPicker')
    canvas.width = width
    canvas.height = height
    this.ctx = canvas.getContext('2d')
    myGradient = this.ctx.createLinearGradient(0, height / 2, width, height / 2)
    if (this.italic) {
      myGradient = this.ctx.createLinearGradient(0, 0, width, height)
    } else if (this.vertical) {
      myGradient = this.ctx.createLinearGradient(width / 2, 0, width / 2, height)
    } else if (this.ritalic) {
      myGradient = this.ctx.createLinearGradient(width, 0, 0, height)
    }
    for (let i = 0; i < len; i++) {
      myGradient.addColorStop(i / len, this.colors[i])
    }
    this.ctx.fillStyle = myGradient
    this.ctx.fillRect(0, 0, width, height)
  },
  methods: {
    hdleMove ({ offsetX, offsetY }) {
      let imgData = this.ctx.getImageData(offsetX, offsetY, 1, 1).data//  取相对位置的一像素rgba图像信息
      this.color = `rgb(${imgData[0]},${imgData[1]},${imgData[2]})`
    },
    hdleClick () {
      this.show = false
      this.$emit('pick-color', this.color)
    }
  }
}
</script>
<style lang="scss">
  .my-color-picker {
    position: relative;
    cursor: pointer;

    .pick {
      position: absolute;
      right: 100%;
      color: black;
      background: white;
      cursor:default;
    }

    .pickArea {
      position: absolute;
      top: 100%;
      cursor: crosshair;
    }
  }
</style>
