<template>
  <img src="https://www.wetools.com/imgplaceholder/800x240" alt="" v-lazy>
</template>

<script>
import Vue from 'vue';
const Lazy = {
    install(Vue, options={}){
        const defaultSrc = options.defaultSrc || 'https://img.zcool.cn/community/01114d59941891000000212989593d.gif'
        Vue.directive('lazy', {
            bind(el) {
                el.ob = Lazy.init(el, defaultSrc);
            },
            unbind(el) {
                el.ob.unobserve(el);
            }
        })
    },
    init(el, defaultSrc) {
        el.dataset.src = el.src;
        el.src = defaultSrc;
        return Lazy.observe(el);
    },
    observe(el) {
        const ob = new IntersectionObserver((enties) => {
            if (enties[0].isIntersecting && el.dataset.src) {
                el.src = el.dataset.src;
                delete el.dataset.src;
            }
        });
        ob.observe(el);
        return ob;
    },
}
Vue.use(Lazy, {
    defaultSrc: 'https://img.zcool.cn/community/01114d59941891000000212989593d.gif'
});
export default {

}
</script>

<style>

</style>