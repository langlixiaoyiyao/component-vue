# LoadMore组件

### 说明
该组件是：上拉加载更多组件，基于web接口的IntersectionObserver构造函数实现的。

### 效果   
<template>
    <demo-load-more />
</template>

### 基本使用   
```vue
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
```

### 参数
#### LoadMore 参数
| 参数名 | 说明 | 类型 | 默认值 |
| --- | ---- | ---- | ----- |
| ref | 获取loadmore组件的实例对象（通过调用其实例对象的loadEnd方法来告诉loadmore组件是否数据加载结束） | - | - |
| onLoadMore | 当loadmore组件出现在窗口可视范围内触发（用来请求数据） | async function | - |


