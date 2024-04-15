<template>
  <van-tab :title="title" v-bind="componentProps">
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
    componentProps: {
      type: Object,
      default: () => {},
    }
  },
};
</script>

<style>
</style>