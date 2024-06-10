<template>
  <button v-throttle:click="handler">假装点击我提交表单</button>
</template>
<script>
export default {
    directives: {
        throttle: {
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
        }
    },
    methods: {
        handler() {
            console.log("点击了")
        },
    },
}
</script>