<template>
  <transition name="slide-down">
    <div class="title-wrapper" v-show="ifTitleAndMenu">
      <div class="left">
        <span class="iconfont icon-xiazai6"></span>
      </div>
      <div class="right">
        <div class="icon-wrapper">
          <span class="iconfont icon-cart"></span>
        </div>
        <div class="icon-wrapper">
          <span class="iconfont icon-person"></span>
        </div>
        <div class="icon-wrapper">
          <span class="iconfont icon-more"></span>
        </div>
      </div>
    </div>
  </transition>
</template>
<script>
export default {
  props: {
    ifTitleAndMenu: {
      type: Boolean,
      default: false
    }
  }
}
</script>
<style lang="scss" scoped>
@import '../assets/styles/gloabal.scss';
.title-wrapper {
  position: absolute;
  top: 0;
  left: 0;
  display: flex;
  z-index: 101;
  width: 100%;
  height: px2rem(150);
  box-shadow: 0 px2rem(20) px2rem(20) rgba(0, 0, 0, 0.15);
  background: white;
  .left {
    flex: 0 0 px2rem(20);
    @include center;
  }
  .right {
    flex: 1;
    display: flex;
    justify-content: flex-end;
    .icon-wrapper {
      flex: 0 0 px2rem(180);
      @include center;
      .icon-cart {
        font-size: px2rem(100)
      }
    }

  }
}
</style>

