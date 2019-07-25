<template>
  <div id="appa">
    <template v-for="(item, index) in d"  >
      <div :key="'button' + index">
        缩放：<input type="range"
          @mousemove="(e) => { m_changeScale(e, item) }"
          @change="(e) => { m_changeScale(e, item) }"
          name="points"
          min="0.5"
          max="2"
          step="0.1"
          value="1">
        旋转：<input type="range"
          @mousemove="(e) => { m_changeRotation(e, item) }"
          @change="(e) => { m_changeRotation(e, item) }"
          name="points"
          min="0"
          max="360"
          step="1"
          value="0">
        <button @click="m_click(item)">裁剪</button>
      </div>
      <div :key="'VueHammerjsImage' + index" style="display: inline-block">
        <VueHammerjsImage
          img="static/logo.png"
          :targetWidth = "item.targetWidth"
          :targetHeight = "item.targetHeight"
          :ref = "'VueHammerjsImage' + item.id"
          :translate3dInfo = "item.translate3dInfo"
          >
        </VueHammerjsImage>
      </div>
      <img :key="'img' + index"
        :src = "item.showSrc"
        :style = "{ width: item.targetWidth + 'px', height: item.targetHeight + 'px' }">
    </template>
  </div>
</template>

<script>
import VueHammerjsImage from 'vue-hammerjs-image/src/vue-hammerjs-image/vue-hammerjs-image.vue'

export default {
  components: {
    VueHammerjsImage
  },
  name: 'appa',
  data () {
    return {
      d: [{
        id: 0,
        targetWidth: 100,
        targetHeight: 200,
        translate3dInfo: {
          rotation: 0,
          scale: 1,
          offset_x: 0,
          offset_y: 0
        },
        showSrc: ''
      }, {
        id: 1,
        targetWidth: 200,
        targetHeight: 200,
        translate3dInfo: {
          rotation: 0,
          scale: 1,
          offset_x: 0,
          offset_y: 0
        },
        showSrc: ''
      }]
    }
  },
  methods: {
    m_changeScale (e, item) {
      item.translate3dInfo.scale = e.target.value
    },
    m_changeRotation (e, item) {
      this.$refs['VueHammerjsImage' + item.id][0].setTranslate3dInfoPreview({ rotation: e.target.value })
    },
    m_click (item) {
      item.showSrc = this.$refs['VueHammerjsImage' + item.id][0].getBase64()
    }
  }
}
</script>

<style>
#appa {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
