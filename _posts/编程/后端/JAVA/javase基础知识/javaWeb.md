### ajax请求    

[参考]: https://blog.csdn.net/Louiser_go/article/details/102858801

```javascript
主要有个参数
url: 请求路劲
contentType: 请求数据编码 application/json;charset=UTF-8
data: 请求的数据 
dataType 请求数据类型 json
type: 请求类型
```

### json对象和json字符串的转化

```javascript
JSON.parse()  将字符串转化为对象  返回对象
JSON.stringify() 将对象转化为字符串  返回字符串
```

### @RequestBody

```java
如果想使用这个注解  则引入fastjson 或者 Gjson

<dependency>
     <groupId>com.alibaba</groupId>
     <artifactId>fastjson</artifactId>
     <version> 1.2.70</version>
</dependency>
```
