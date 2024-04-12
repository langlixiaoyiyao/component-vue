<template>
  <van-tabs v-model="active">
    <slot></slot>
  </van-tabs>
</template>

<script>
import { Tabs } from "vant";
import "vant/lib/tabs/style/index";
export default {
  components: {
    [Tabs.name]: Tabs,
  },
  data() {
    return {
      active: 0,
    }
  },
  props: ['activeIndex'],
  watch: {
    activeIndex: function (newVal, oldVal) {
      this.active = newVal;
    },
  },
};
</script>

<style lang="less">
.van-tabs {
  background-color: rgb(54, 128, 246);
  border-radius: 10px;
  overflow: hidden;
  padding-top: 10px;
  .van-tabs__nav {
    background-color: transparent;
    .van-tab {
      border-radius: 10px 10px 0 0;
      position: relative;
      &::before,
      &::after {
        border-radius: 10px 10px 0 0;
        right: -20px;
        top: 0;
        position: absolute;
        display: block;
        content: "";
        height: 62px;
        width: 40px;
        background-color: #fff;
        transform: rotateZ(-45deg);
      }
      &.van-tab--active {
        background-color: #fff;
      }
    }
    .van-tabs__line {
      display: none;
    }
  }
  .van-tabs__content {
    .van-tab__pane {
      background-color: #fff;
    }
  }
}
</style>