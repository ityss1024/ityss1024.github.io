

示例

修改app.vue 页面

```javascript
// 注意  只有一个router-view可以给name值  即默认 其他router-view必须给name值
<router-view/>
<router-view name="left" style="float:left;width:50%;height:300px;background-color:#ccc;"></router-view>
<router-view name="right" style="float:left;width:50%;height:300px;background-color:#c0c;"></router-view>
```

修改index.js

```javascript
{
    path: '/',
    name: 'HelloWorld',
    // 注意  是components 多了一个s
    components: {
        default: HelloWorld,
        left: Hi1,
        right: Hi2
    }
}
```

