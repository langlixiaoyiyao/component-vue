## 自定义指令之防止表达重复提交

### 定义指令
```js
Vue.directive('throttle', {
    bind(el, binding) {
        el.handler = function (e) {
            e.stopImmediatePropagation();
            if (cbFn) {
                clearTimeout(cbFn);
            }
            cbFn = setTimeout(() => {
                cbFn = null;
                handler();
            }, time);
        }
        let cbFn = null;
        let { time, handler } = (typeof binding.value === 'function' ? {
            time: 300,
            handler: binding.value
        } : binding.value);
        el.addEventListener(binding.arg, el.handler, true);
    },
    unbind(el) {
        el.removeEventListener('click', el.handler);
    }
})
```

### 使用
```html
<template>
    <span class="shop_header_title" v-throttle:click="handler" >附近商家</span>
<template>
<script>
    export default {
        methods: {
            handler() {
                ....
            }
        }
    }
</script>
```