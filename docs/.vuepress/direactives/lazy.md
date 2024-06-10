## 自定义指令之图片懒加载

### 定义插件
```js
const Lazy = {
    install(Vue, options={}){
        const defaultSrc = options.defaultSrc || 'https://www.wetools.com/imgplaceholder/800x240'
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
Vue.use(Lazy);
```

### 使用插件
```html
<img class="shop_img" :src="imgBaseUrl + item.image_path" v-lazy>
```