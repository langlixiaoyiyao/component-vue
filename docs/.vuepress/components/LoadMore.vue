<template>
  <div class="load_more" ref="loadMoreRef">
    <div class="loading_end" v-if="end">没有更多了~</div>
    <div class="loading" v-if="loading">加载中...</div>
    <div class="will_load" v-if="!loading && !end" @click="loadData">
      加载更多
    </div>
  </div>
</template>
<script>
export default {
  props: ["onLoadMore"],
  data() {
    return {
      end: false,
      loading: false,
      observe: null,
    };
  },
  methods: {
    loadEnd(flag = true) {
      this.end = flag;
    },
    async loadData() {
      if (!this.end && !this.loading) {
        this.loading = true;
        await this.onLoadMore();
        this.loading = false;
      }
    },
  },
  mounted() {
    this.observe = new IntersectionObserver((entries) => {
      if (entries[0].intersectionRect.bottom > 0) {
        this.loadData();
      }
    });
    this.observe.observe(this.$refs.loadMoreRef);
  },
  destroyed() {
    this.observe.unobserve(this.$ref.loadMoreRef);
  },
};
</script>
<style lang="less">
.load_more {
  display: flex;
  justify-content: center;
  padding: 0.3rem 0;
  .loading_end {
    color: #666;
  }
  .loading {
    color: green;
  }
  .will_load {
    cursor: pointer;
    color: green;
  }
}
</style>