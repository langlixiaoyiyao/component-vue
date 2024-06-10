<template>
<div class="need_copy_container" v-copy>
    <div>哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈哈</div>
</div>
</template>

<script>
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
export default {

}
</script>

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