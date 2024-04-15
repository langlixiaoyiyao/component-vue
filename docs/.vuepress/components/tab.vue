<template>
  <van-tab :title="title">
    <slot>标签</slot>
  </van-tab>
</template>

<script>
import { Tab } from "vant";
import "vant/lib/tab/style/index";
export default {
  components: {
    [Tab.name]: Tab,
  },
  props: {
    title: {
      type: String,
      default: "标签",
    },
  },
};
</script>

<style>
</style>