# v-throttle指令

### 说明
用于防止表单同一时间段内触发点击多次，导致多次提交

### 效果   
<template>
    <demo-throttle />
</template>

### 基本使用
```vue
<template>
<div v-throttle:click="handler">假装点击我提交表单</div>
</template>
<script>
export default {
    methods: {
        handler() {
            console.log("点击了")
        },
    },
}
</script>
```

### 参数
指令参数：代表触发的事件，比如click、submit   
指令值：Object | Fucntion，如果是function代表点击后要触发的处理函数，如果是object，格式为{time：时间，handler：处理函数}


