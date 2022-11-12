### 添加相关的maven依赖

```xml
<dependency>
    <groupId>cn.hutool</groupId>
    <artifactId>hutool-all</artifactId>
    <version>5.8.2</version>
</dependency>
```

### 官网：https://www.hutool.cn/

### StrUtil 字符串工具类

```java
//判断是否为空字符串
String str = "test";

StrUtil.isEmpty(str);
StrUtil.isNotEmpty(str);
StrUtil.isBlank(str);
isBlank() 会把不可见字符也算作空  更严格
String str = "          ";
System.out.println(StrUtil.isBlank(str));  // true
System.out.println(StrUtil.isEmpty(str));  // false
//去除字符串的前后缀
StrUtil.removeSuffix("a.jpg", ".jpg");
StrUtil.removePrefix("a.jpg", "a.");
//格式化字符串
String template = "这只是个占位符:{}";
String str2 = StrUtil.format(template, "我是占位符");
LOGGER.info("/strUtil format:{}", str2);
```

### CollUtil 集合操作类

```java
//数组转换为列表
String[] array = new String[]{"a", "b", "c", "d", "e"};
List<String> list = CollUtil.newArrayList(array);
//join：数组转字符串时添加连接符号
String joinStr = CollUtil.join(list, ",");
LOGGER.info("collUtil join:{}", joinStr);
//将以连接符号分隔的字符串再转换为列表
List<String> splitList = StrUtil.split(joinStr, ',');
LOGGER.info("collUtil split:{}", splitList);
//创建新的Map、Set、List
HashMap<Object, Object> newMap = CollUtil.newHashMap();
HashSet<Object> newHashSet = CollUtil.newHashSet();
ArrayList<Object> newList = CollUtil.newArrayList();
//判断列表是否为空
CollUtil.isEmpty(list);
```

### MapUtil Map操作工具类

```java
//将多个键值对加入到Map中
Map<Object, Object> map = MapUtil.of(new String[][]{
    {"key1", "value1"},
    {"key2", "value2"},
    {"key3", "value3"}
});
//判断Map是否为空
MapUtil.isEmpty(map);
MapUtil.isNotEmpty(map);
```

### SecureUtil 加密解密工具类

```javascript
// md5摘要加密
String md5 = SecureUtil.md5("abc");

// sha1摘要加密
String sha1 = SecureUtil.sha1("abc");

// 生成非对称密钥对
KeyPair keyPair = SecureUtil.generateKeyPair("RSA");
String publicKey = Base64Encoder.encode(keyPair.getPublic().getEncoded());
String privateKey = Base64Encoder.encode(keyPair.getPrivate().getEncoded());

// 利用公钥加密
String encryptBase64 = SecureUtil.rsa(privateKey, publicKey).encryptBase64("abc", KeyType.PublicKey);

// 利用私钥解密
String decrypt = new String(SecureUtil.rsa(privateKey, publicKey).decrypt(encryptBase64, KeyType.PrivateKey));
```

### CaptchaUtil 验证码工具类 做图形验证

```java
//生成验证码图片
LineCaptcha lineCaptcha = CaptchaUtil.createLineCaptcha(200, 100);
try {
    request.getSession().setAttribute("CAPTCHA_KEY", lineCaptcha.getCode());
    response.setContentType("image/png");//告诉浏览器输出内容为图片
    response.setHeader("Pragma", "No-cache");//禁止浏览器缓存
    response.setHeader("Cache-Control", "no-cache");
    response.setDateHeader("Expire", 0);
    lineCaptcha.write(response.getOutputStream());
} catch (IOException e) {
    e.printStackTrace();
}
```

### Convert 类型转换类

```java
//转换为字符串
int a = 1;
String aStr = Convert.toStr(a);
//转换为指定类型数组
String[] b = {"1", "2", "3", "4"};
Integer[] bArr = Convert.toIntArray(b);
//转换为日期对象
String dateStr = "2017-05-06";
Date date = Convert.toDate(dateStr);
//转换为列表
String[] strArr = {"a", "b", "c", "d"};
List<String> strList = Convert.toList(String.class, strArr);
```

### DateUtil 日期时间工具类

```java
//Date、long、Calendar之间的相互转换
//当前时间
Date date = DateUtil.date();
//Calendar转Date
date = DateUtil.date(Calendar.getInstance());
//时间戳转Date
date = DateUtil.date(System.currentTimeMillis());
//自动识别格式转换
String dateStr = "2017-03-01";
date = DateUtil.parse(dateStr);
//自定义格式化转换
date = DateUtil.parse(dateStr, "yyyy-MM-dd");
//格式化输出日期
String format = DateUtil.format(date, "yyyy-MM-dd");
//获得年的部分
int year = DateUtil.year(date);
//获得月份，从0开始计数
int month = DateUtil.month(date);
//获取某天的开始、结束时间
Date beginOfDay = DateUtil.beginOfDay(date);
Date endOfDay = DateUtil.endOfDay(date);
//计算偏移后的日期时间
Date newDate = DateUtil.offset(date, DateField.DAY_OF_MONTH, 2);
//计算日期时间之间的偏移量
long betweenDay = DateUtil.between(date, newDate, DateUnit.DAY);
```

### NumberUtil 数字处理类

```java
double n1 = 1.234;
double n2 = 1.234;
double result;
//对float、double、BigDecimal做加减乘除操作
result = NumberUtil.add(n1, n2);
result = NumberUtil.sub(n1, n2);
result = NumberUtil.mul(n1, n2);
result = NumberUtil.div(n1, n2);
//保留两位小数
BigDecimal roundNum = NumberUtil.round(n1, 2);
String n3 = "1.234";
//判断是否为数字、整数、浮点数
NumberUtil.isNumber(n3);
NumberUtil.isInteger(n3);
NumberUtil.isDouble(n3);
```

### FileUtil 文件操作类

```java
if(!FileUtil.exist("D:\\test.txt")){
    // 创建文件
    FileUtil.touch(new File("D:\\test.txt"));
    // 写入内容
    FileWriter writer = new FileWriter("D:\\test.txt");
    int i = 0;
    while (i<10){
        writer.append(i+",");
        i++;
    }
} else {
    // 读取文件内容
    FileReader fileReader = new FileReader("D:\\test.txt");
    String result = fileReader.readString();
    if (StrUtil.isNotBlank(result)){
        System.out.println(result);
    }
}
// h
```

### ExeclUtil Execl操作

```java
// 将文件转换为ExcelReader
ExcelReader reader = ExcelUtil.getReader("d:/aaa.xlsx");

// 读取所有行和列的数据
List<List<Object>> data = reader.read();

// 读取为Map列表，默认excel第一行为标题行，Map中的key为标题，value为标题对应的单元格值。
List<Map<String,Object>> dataMap = reader.readAll();

//创建writer
ExcelWriter writer = ExcelUtil.getWriter("d:/bbb.xlsx");

// 数据量特别大时，使用BigExcelWriter对象，可以避免内存溢出
ExcelWriter bigWriter = ExcelUtil.getBigWriter("d:/bbb.xlsx");

// 构造数据
List<String> row1 = CollUtil.newArrayList("aa", "bb", "cc", "dd");
List<String> row2 = CollUtil.newArrayList("aa1", "bb1", "cc1", "dd1");
List<String> row3 = CollUtil.newArrayList("aa2", "bb2", "cc2", "dd2");
List<String> row4 = CollUtil.newArrayList("aa3", "bb3", "cc3", "dd3");
List<String> row5 = CollUtil.newArrayList("aa4", "bb4", "cc4", "dd4");
List<List<String>> rows = CollUtil.newArrayList(row1, row2, row3, row4, row5);

// 一次性将数据写入excel中
writer.write(rows, true);
```

