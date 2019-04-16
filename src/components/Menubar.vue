<template>
  <div class="menu-bar">
    <transition name="slide-up">
      <div class="menu-wrapper" v-show="ifTitleAndMenu" :class="{'hide-box-shabow': ifSettingShow || !ifTitleAndMenu}">
        <div class="icon-wrapper">
          <span class="iconfont icon-menu"></span>
        </div>
        <div class="icon-wrapper">
          <span class="iconfont icon-3jingdu"></span>
        </div>
        <div class="icon-wrapper">
          <span class="iconfont icon-ai250" @click="showSetting(1)"></span>
        </div>
        <div class="icon-wrapper">
          <span class="iconfont" @click="showSetting(0)">A</span>
        </div>
      </div>
    </transition>
    <transition name="slide-up">
      <div class="setting-wrapper" v-show="ifSettingShow">
        <div class="setting-font-size" v-if="showTag === 0">
          <div class="preview" :style="{fontSize: fontSizeList[0].fontSize + 'px'}">A</div>
          <div class="slect">
            <div class="slect-wrapper" v-for="(item, index) in fontSizeList" :key="index" @click="setFontSize(item.fontSize)">
              <div class="line"></div>
              <div class="point-wrapper">
                <div class="point" v-show="defaultFontSize == item.fontSize">
                  <div class="small-point"></div>
                </div>
              </div>
              <div class="line"></div>
            </div>
          </div>
          <div class="preview" :style="{fontSize: fontSizeList[fontSizeList.length-1].fontSize + 'px'}">A</div>
        </div>
        <div class="setting-theme" v-else-if="showTag === 1">
          <div class="setting-theme-item" v-for="(item, index) in themeList" :key="index" @click="setTheme(index)">
            <div class="preview" :style="{background: item.style.body.background}" :class="{'no-border': item.style.body.background != '#fff'}"></div>
            <div class="text" :class="{'selected': index === defaultTheme}">{{ item.name }}</div>
          </div>
        </div>
      </div>
    </transition>
  </div>
</template>
<script>
export default {
  data() {
    return {
      ifSettingShow: false,
      showTag: 0
    }
  },
  methods: {
    setTheme(index) {
      this.$emit('setTheme', index)
    },
    showSetting(tag) {
      this.ifSettingShow = true
      this.showTag = tag
    },
    hideSetting() {
      this.ifSettingShow = false
    },
    setFontSize(fontSize) {
      this.$emit('setFontSize', fontSize)
    }
  },
  props: {
    ifTitleAndMenu: {
      type: Boolean,
      default: false
    },
    fontSizeList: Array,
    defaultFontSize: Number,
    themeList: Array,
    defaultTheme: Number
  }
}
</script>
<style lang="scss" scoped>
@import '../assets/styles/gloabal.scss';
.menu-bar {
  .menu-wrapper {
    position: absolute;
    bottom: 0;
    left: 0;
    display: flex;
    z-index: 101;
    width: 100%;
    height: px2rem(150);
    background: white;
    box-shadow: 0 px2rem(-20) px2rem(20) rgba(0, 0, 0, 0.15);
    &.hide-box-shabow {
      box-shadow: none
    }
    .icon-wrapper {
      flex: 1;
      @include center;
      .icon-ai250 {
        font-size: px2rem(100)
      }
    }
  }
  .setting-wrapper {
    position: absolute;
    bottom: px2rem(150);
    left: 0;
    width: 100%;
    height: px2rem(150);
    background: white;
    box-shadow: 0 px2rem(-8) px2rem(8) rgba(0, 0, 0, 0.15);
    z-index: 101;
    .setting-font-size {
      display: flex;
      width: 100%;
      height: px2rem(200);
      .preview {
        flex: 0 0 px2rem(80);
        @include center;
      }
      .slect {
        display: flex;
        flex: 1;
        .slect-wrapper {
          flex: 1;
          display: flex;
          align-items: center;
          &:first-child {
            .line {
              &:first-child {
                border-top: none;
              }
            }
          }
          &:last-child {
            .line {
              &:last-child {
                border-top: none;
              }
            }
          }
          .line {
            flex: 1;
            height: 0;
            border-top: px2rem(1) solid #cccccc;
          }
          .point-wrapper {
            flex: 0 0 0;
            width: 0;
            height: px2rem(14);
            border-left: px2rem(1) solid #cccccc;
            position: relative;
            .point {
              position: absolute;
              top: px2rem(-16);
              left: px2rem(-16);
              width: px2rem(40);
              height: px2rem(40);
              border-radius: 50%;
              background: white;
              border: px2rem(1) solid #cccccc;
              box-shadow: 0 px2rem(4) px2rem(4) rgba(0, 0, 0, 0.15);
              @include center;
              .small-point {
                width: px2rem(10);
                height: px2rem(10);
                border-radius: 50%;
                background: black;
              }
            }
          }
        }
      }
    }
    .setting-theme {
      width: 100%;
      display: flex;
      .setting-theme-item {
        flex: 1;
        display: flex;
        flex-direction: column;
        padding: px2rem(10);
        .preview {
          flex: 1;
          height: px2rem(80);
          border: px2rem(1) solid #cccccc;
          &.no-border {
            border: none;
          }
        }
        .text {
          flex: 0 0 px2rem(60);
          font-size: px2rem(20);
          color: #cccccc;
          height: px2rem(200);
          @include center;
          &.selected {
            color: #333;
          }
        }
      }
    }
  }
}

</style>

