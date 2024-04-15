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
      active: 1,
    };
  },
  props: ["activeIndex"],
  watch: {
    activeIndex: function (newVal, oldVal) {
      this.active = newVal;
    },
  },
};
</script>

<style lang="less">
.van-tabs {
  background-color: rgb(54, 128, 246);    // 背景色
  border-radius: 10px;
  overflow: hidden;
  padding-top: 10px;
  .van-tabs__nav {
    background-color: transparent;
    .van-tab {
      color: #fff;
      position: relative;
      &::before,
      &::after {
        z-index: 2;
        position: absolute;
        display: block;
        content: "";
        background-color: rgb(54, 128, 246); // 背景色
        width: 15px;
        height: 100%;
      }
      &::before {
        left: 0;
        border-bottom-left-radius: 12px;
        transform: skewX(15deg);
      }
      &::after {
        right: 0;
        border-bottom-right-radius: 12px;
        transform: skewX(-15deg)
      }
      &.van-tab--active {
        background-color: #fff;   // 活跃色
        box-shadow: 15px 22px 0 #fff, -15px 22px 0 #fff; // 颜色：活跃色，22px是tabnav的高度的一半，15px是伪元素的宽度
        color: #333;
        &::before,
        &::after {
          background-color: #fff; // 活跃色
          transform: skewX(-15deg)
        }
        &::before {
          left: 0px;
          background-color: #fff; // 活跃色
          box-shadow: -1px -22px 0 rgb(54, 128, 246), -15px -22px 0 rgb(54, 128, 246);  // 颜色：背景色，22px是tabnav的高度的一半，15px是伪元素的宽度
          border-top-left-radius: 12px;
          border-bottom-left-radius: 0;
        }
        &::after {
          transform: skewX(15deg);
          right: 0px;
          background-color: #fff;  // 活跃色
          box-shadow: 15px -22px 0 rgb(54, 128, 246), 1px -22px 0 rgb(54, 128, 246); // 颜色：背景色，22px是tabnav的高度的一半，15px是伪元素的宽度
          border-top-right-radius: 12px;
          border-bottom-right-radius: 0;
        }
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