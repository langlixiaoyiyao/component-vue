# tab组件

### 说明
该组件是基于vant ui库的tabs实现的封装。用于移动端

### 效果   
<br>
<tabs :activeIndex="1">
    <tab title="昨日" :componentProps="{}">昨日</tab>
    <tab title="近七天">近七天</tab>
    <tab title="近三十天">近三十天</tab>
    <tab title="近180天">近180天</tab>
</tabs>

### 基本使用
```
<tabs :activeIndex="1">
    <tab title="昨日" :componentProps="{}">昨日</tab>
    <tab title="近七天">近七天</tab>
    <tab title="近三十天">近三十天</tab>
    <tab title="近180天">近180天</tab>
</tabs>
```

### 参数
#### tabs 参数
| 参数名 | 说明 | 类型 | 默认值 |
| --- | ---- | ---- | ----- |
| activeIndex | 活跃的tab | Number | 0 |
| componentsProps | vant组件库支持的tabs的所有参数 | Object | - |

#### tab参数
| 参数名 | 说明 | 类型 | 默认值 |
| --- | ---- | ---- | ----- |
| title | 标题 | String | `标签` |
| componentsProps | vant组件库支持的tab的所有参数 | Object | - |

