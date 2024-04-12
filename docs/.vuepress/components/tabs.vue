<template>
  <van-tabs>
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
};
</script>

<style>
</style>