<template>
    <div>
        <div class="list">
            <div class="item" v-for="(item, index) in shops" :key="index">{{item}}</div>
        </div>
        <load-more ref="loadRef" :onLoadMore="onLoadMore" />
    </div>
</template>
<script>
export default {
    data() {
        return {
            shops: [1, 2, 3],
        }
    },
    methods: {
        async onLoadMore() {
            const res = await new Promise((resolve) => {
                setTimeout(() => {
                    resolve([1,2,3,4]);
                }, 300)
            });
            if (res.length > 0) {
                this.shops = [...this.shops, ...res];
            } else {
                this.$refs.loadRef && this.$refs.loadRef.loadEnd();
            }
        }
    },
}
</script>