<template>
  <div class="ebook">
    <dir class="read-wrapper">
      <div id="read"></div>
    </dir>
  </div>
</template>
<script>
import Epub from 'epubjs'
const DOWNLOAD_URL = '/static/167176.epub'
global.ePub = Epub
export default {
  methods: {
    // 电子书的解析和渲染
    showEpub() {
      // 生成Book
      this.book = new Epub(DOWNLOAD_URL)
      // 生成Rendition
      this.rendition = this.book.renderTo('read', {
        width: window.innerWidth,
        height: window.innerHeight
      })
      // 通过Rendtin.display渲染电子书
      this.rendition.display()
    }
  },
  mounted() {
    this.showEpub()
  }
}
</script>
<style lang="sass" scoped>

@import 'assets/styles/gloabal.scss'

</style>


