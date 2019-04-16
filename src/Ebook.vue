<template>
  <div class="ebook">
    <TitleBar
    :ifTitleAndMenu='ifTitleAndMenu'
    ></TitleBar>
    <div class="read-wrapper">
      <div id="read"></div>
      <div class="mask">
        <div class="left" @click="prevPage"></div>
        <div class="center" @click="toogleTitleAndMenu"></div>
        <div class="right" @click="nextPage"></div>
      </div>
    </div>
    <Menubar
    :ifTitleAndMenu='ifTitleAndMenu'
    :fontSizeList='fontSizeList'
    :defaultFontSize= 'defaultFontSize'
    @setFontSize="setFontSize"
    :themeList='themeList'
    :defaultTheme='defaultTheme'
    @setTheme='setTheme'
    ref="menuBar"
    ></Menubar>
  </div>
</template>
<script>
import Epub from 'epubjs'
import TitleBar from './components/TitleBar'
import Menubar from './components/MenuBar'
const DOWNLOAD_URL = '/static/167176.epub'
global.ePub = Epub
export default {
  components: {
    TitleBar,
    Menubar
  },
  data () {
    return {
      ifTitleAndMenu: false,
      fontSizeList: [
        {fontSize: 12},
        {fontSize: 14},
        {fontSize: 16},
        {fontSize: 18},
        {fontSize: 20},
        {fontSize: 22},
        {fontSize: 24}
      ],
      defaultFontSize: 16,
      themeList: [
        {
          name: 'default',
          style: {
            body: {
              'color': '#000',
              'background': '#fff'
            }
          }
        },
        {
          name: 'eye',
          style: {
            body: {
              'color': '#000',
              'background': '#ceeaba'
            }
          }
        },
        {
          name: 'night',
          style: {
            body: {
              'color': '#fff',
              'background': '#000'
            }
          }
        },
        {
          name: 'gold',
          style: {
            body: {
              'color': '#000',
              'background': 'rgb(241, 236, 226)'
            }
          }
        }
      ],
      defaultTheme: 0
    }
  },
  methods: {
    // 设置默认主题
    setTheme(index) {
      this.themes.select(this.themeList[index].name)
      this.defaultTheme = index
    },
    // 注册主题
    registerTheme () {
      this.themeList.forEach(theme => {
        this.themes.register(theme.name, theme.style)
      })
    },
    setFontSize(fontSize) {
      this.defaultFontSize = fontSize
      if (this.themes) {
        this.themes.fontSize(fontSize + 'px')
      }
    },
    toogleTitleAndMenu() {
      this.ifTitleAndMenu = !this.ifTitleAndMenu
      if (!this.ifTitleAndMenu) {
        this.$refs.menuBar.hideSetting()
      }
    },
    prevPage() {
      // rendition.prev
      if (this.rendition) {
        this.rendition.prev()
      }
    },
    nextPage() {
      // Rendition.next
      if (this.rendition) {
        this.rendition.next()
      }
    },
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
      // 获取thems
      this.themes = this.rendition.themes
      // 设置默认字体
      this.setFontSize(this.defaultFontSize)
      // this.themes.register(name, style)
      // this.setTheme(this.defaultTheme)
      this.registerTheme()
      // 设置默认主题
      this.setTheme(this.defaultTheme)
    }
  },
  mounted() {
    this.showEpub()
  }
}
</script>
<style lang="scss" scoped>
@import 'assets/styles/gloabal.scss';
.ebook {
  position: relative;
  .read-wrapper {
    .mask {
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      display: flex;
      z-index: 100;
      .left {
        flex: 0 0  px2rem(200);
      }
      .center {
        flex: 1;
      }
      .right {
        flex: 0 0  px2rem(200);
      }
    }
  }
}
</style>


