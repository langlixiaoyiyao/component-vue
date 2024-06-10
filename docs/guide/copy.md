# v-copy指令

### 说明
用于实现一键复制

### 效果   
<template>
    <demo-copy />
</template>

### 基本使用
```js
import Vue from 'vue';
Vue.directive('copy', {
    bind(el) {
        const dom = document.createElement('div');
        dom.innerText = '点击复制';
        dom.className = 'click_to_click';
        dom.addEventListener('click', () => {
            navigator.clipboard.writeText(el.firstChild.innerText).then(() => {
                dom.innerText = '复制成功';
                setTimeout(() => {
                    dom.innerText = '点击复制';
                }, 3000)
            })
        })
        el.appendChild(dom);
    }
})
```
```vue
<template>
<div class="need_copy_container" v-copy>
    <div>哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈</div>
</div>
</template>
<style>
.need_copy_container {
    width: 300px;
    height: auto;
    background-color: black;
    color: #fff;
    font-size: 20px;
    position: relative;
}

.need_copy_container .click_to_click {
    position: absolute;
    top: 0;
    right: 0;
    padding: 6px;
    color: #333;
    font-size: 14px;
    background: rgba(255, 255, 255, 0.9);
}
</style>
```

### 使用说明
v-copy指令要放在要复制文本标签的父容器上面，复制的是指令所在元素的第一个子元素的innerText



