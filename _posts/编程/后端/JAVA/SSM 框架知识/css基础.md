## 参考资料

> [CSS 参考手册_w3cschool](https://www.w3cschool.cn/cssref/) 
>
> [CSS 教程_w3cschool](https://www.w3cschool.cn/css/) 

## 层叠样式的优先级

> [css层叠性，优先级问题_diligentkong的博客-CSDN博客](https://blog.csdn.net/diligentkong/article/details/54311573?utm_medium=distribute.pc_relevant.none-task-blog-2~default~BlogCommendFromMachineLearnPai2~default-1.control&dist_request_id=1331647.9945.16183847526347007&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2~default~BlogCommendFromMachineLearnPai2~default-1.control) 
>
> 相同的样式后加载的会覆盖已加载的

## 浏览器打印

> 样式丢失：加 !important 即可
>
> a标签路由显示：[(1条消息) 前端打印页面window.print()，会把页面把A标签里面的href属性也给打印出来解决办法_congweijing的博客-CSDN博客](https://blog.csdn.net/congweijing/article/details/108381629) 
>
> [(1条消息) web前端打印需要注意的CSS样式_勤劳并微笑着的博客-CSDN博客](https://blog.csdn.net/qq_37791764/article/details/77970825?utm_medium=distribute.pc_relevant.none-task-blog-baidujs_title-0&spm=1001.2101.3001.4242) 

> `@media print {}` 打印时使用的样式

## 响应式布局

> [响应式 Web 设计 – Viewport_w3cschool](https://www.w3cschool.cn/css/css-rwd-viewport.html) 

## css 识别屏幕大小自适应

> [(1条消息) css 识别屏幕大小自适应_GOODDEEP-CSDN博客_css根据屏幕 适应宽度](https://blog.csdn.net/u013378306/article/details/78840633) 

## 长度单位

- [css中单位em和rem的区别 - _wind - 博客园 (cnblogs.com)](https://www.cnblogs.com/wind-lanyan/p/6978084.html) 

> - 相对单位
>   - em - 相对父元素的字体大小倍数
>   - rem - 相对html元素的字体大小倍数
> - 绝对单位
>   - px - 像素单位

## 计算

> 可以使用`calc()`方法来计算表达式

## 颜色设置方式

> 1.  使用颜色名： 
>
>    ![image-20210827140425972](image-20210827140425972.png) 
>
> 2.  百分比
>
>    rgb(100%, 100%, 100%)
>
>    rgb(212 212 212 / 59%)	这种不适用IE
>
> 3.  数值
>
>    rgb(229, 229, 229)
>
>    rgba(229, 229, 229, 0.7)
>
> 4.  16进制码
>
>    #FFFFFF
>
>    #FFFFFFFF 这种不适用IE

## 透明度

- opacity:0~1;该属性会使内容也一起透明

- background-color:rgba(0,0,0,0~1);该属性使用rgba的最后一个a就是透明度，该透明只对当前背景生效

## 边框 border

```CSS
border:border-width border-style border-color;
border:1px solid #acacac;
```

- border-width：边框宽度

- border-style：风格

  - solid 实线

- border-color：颜色

- border-radius：圆角

  - ```css
    border-radius: 6px 6px 6px 6px;/*左上 右上 右下 左下*/
    ```

## 阴影 box-shadow

- [(19条消息) css3中的box-shadow(阴影)使用说明和兼容性问题_别逗了好么的博客-CSDN博客](https://blog.csdn.net/hutuchongaini/article/details/55671075) 
- [box-shadow - CSS（层叠样式表） | MDN (mozilla.org)](https://developer.mozilla.org/zh-CN/docs/Web/CSS/box-shadow) 

```css
box-shadow: 0px 0px 5px 0px #b4b4b4;/*阴影样式，x偏移量，y偏移量，模糊量，扩张量【阴影样式默认不写，inset是内阴影】*/
```

## 文本相关

### 不可选择

```css
user-select: none;
```

### 去除点击时的背景色

> 建议在body使用
>
> ```css
> -webkit-tap-highlight-color: transparent;
> ```

### 文本框

> textarea

> 禁止拉伸
>
> ```css
> resize: none;
> ```
>

### 自动换行 word-break

> [CSS word-break 属性 (w3school.com.cn)](https://www.w3school.com.cn/cssref/pr_word-break.asp) 

### 文本不换行

```css
white-space: nowrap;
```

| normal   | 默认。空白会被浏览器忽略。                                   |
| -------- | ------------------------------------------------------------ |
| pre      | 空白会被浏览器保留。其行为方式类似 HTML 中的 <pre> 标签。    |
| nowrap   | 文本不会换行，文本会在在同一行上继续，直到遇到 <br> 标签为止。 |
| pre-wrap | 保留空白符序列，但是正常地进行换行。                         |
| pre-line | 合并空白符序列，但是保留换行符。                             |
| inherit  | 规定应该从父元素继承 white-space 属性的值。                  |

### 文字属性

> [(5条消息) HTML —— CSS样式 文字属性_eno的博客-CSDN博客](https://blog.csdn.net/z_e_n_g/article/details/81045781) 

### 字体 font

| *font-style*            | 规定字体样式。参阅：[font-style](https://www.w3school.com.cn/cssref/pr_font_font-style.asp) 中可能的值。 |
| ----------------------- | ------------------------------------------------------------ |
| *font-variant*          | 规定字体异体。参阅：[font-variant](https://www.w3school.com.cn/cssref/pr_font_font-variant.asp) 中可能的值。 |
| *font-weight*           | 规定字体粗细。参阅：[font-weight](https://www.w3school.com.cn/cssref/pr_font_weight.asp) 中可能的值。 |
| *font-size/line-height* | 规定字体尺寸和行高。参阅：[font-size](https://www.w3school.com.cn/cssref/pr_font_font-size.asp) 和 [line-height](https://www.w3school.com.cn/cssref/pr_dim_line-height.asp) 中可能的值。 |
| *font-family*           | 规定字体系列。参阅：[font-family](https://www.w3school.com.cn/cssref/pr_font_font-family.asp) 中可能的值。 |

>   导入字体：
>
>   ```css
>   @font-face {
>       font-family: HeiSASC-Light;
>       src: url("../components/ArticlePreview/Fonts/HeiSASC-Light.TTF");
>   }
>   ```
>
>   使用字体：(在使用时他才会真实的引入字体文件，可以在浏览器的调试器中的网络里面看到)
>
>   ```css
>   * {
>   	font-family: HeiSASC-Light;
>   }
>   ```



## 宽度 width

- 指定固定宽度
- 使用基于父容器的百分比
- inherit 继承父容器的设置
- max-content 根据最大内容宽度设定（IE中不适用，请使用 auto）
- min-content 根据最小内容宽度设定
- fit-content 根据内容宽度自动设定

## 元素显示类型 display

| none               | 此元素不会被显示。                                           |
| ------------------ | ------------------------------------------------------------ |
| block              | 此元素将显示为块级元素，此元素前后会带有换行符。             |
| inline             | 默认。此元素会被显示为内联元素，元素前后没有换行符。         |
| inline-block       | 行内块元素。（CSS2.1 新增的值）                              |
| list-item          | 此元素会作为列表显示。                                       |
| run-in             | 此元素会根据上下文作为块级元素或内联元素显示。               |
| compact            | CSS 中有值 compact，不过由于缺乏广泛支持，已经从 CSS2.1 中删除。 |
| marker             | CSS 中有值 marker，不过由于缺乏广泛支持，已经从 CSS2.1 中删除。 |
| table              | 此元素会作为块级表格来显示（类似 <table>），表格前后带有换行符。 |
| inline-table       | 此元素会作为内联表格来显示（类似 <table>），表格前后没有换行符。 |
| table-row-group    | 此元素会作为一个或多个行的分组来显示（类似 <tbody>）。       |
| table-header-group | 此元素会作为一个或多个行的分组来显示（类似 <thead>）。       |
| table-footer-group | 此元素会作为一个或多个行的分组来显示（类似 <tfoot>）。       |
| table-row          | 此元素会作为一个表格行显示（类似 <tr>）。                    |
| table-column-group | 此元素会作为一个或多个列的分组来显示（类似 <colgroup>）。    |
| table-column       | 此元素会作为一个单元格列显示（类似 <col>）                   |
| table-cell         | 此元素会作为一个表格单元格显示（类似 <td> 和 <th>）          |
| table-caption      | 此元素会作为一个表格标题显示（类似 <caption>）               |
| inherit            | 规定应该从父元素继承 display 属性的值。                      |
| flex               | 弹性布局，设为Flex布局以后，子元素的float、clear和vertical-align属性将失效。 |

## 元素布局

### 弹性布局 `flex`

> **flex容器**中子元素的 `margin-top`、`margin-bottom` 才会生效

```css
display: flex;
```

> **flex容器属性：** 
>
> - flex-direction: 设置主轴
>   - row x轴为主轴
>   - column y轴为主轴
>   - row-reverse x轴为主轴，反向
>   - column-reverse y轴为主轴，反向
>
> - justify-content: 主轴对齐方式
>   - flex-start 头部对齐【若主轴是x轴则左对齐】
>   - flex-end 尾部对齐
>   - center 居中对齐
>   - space-between 居中对齐并除去边缘外平分剩余空间
> - align-items: 侧轴对齐方式 - 单行生效【若主轴是y轴则单列生效】
>   - flex-start 头部对齐【若主轴是x轴则顶部对齐】
>   - flex-end 尾部对齐
>   - center 居中对齐
> - align-content: 侧轴对齐方式 - 多行生效【若主轴是y轴则多列生效】
>   - flex-start 头部对齐【若主轴是x轴则顶部对齐】
>   - flex-end 尾部对齐
>   - center 居中对齐
>   - space-between 居中对齐并除去边缘外平分剩余空间
>
> - flex-wrap: 设置是否换行 - 默认nowrap
>   - wrap 换行
>   - nowrap 不换行
>
> **flex容器子元素属性：** 
>
> - flex: 设置子元素在主轴方向的剩余空间占比，
>   - <number> 占比权重
>   - auto
> - align-self: 子元素的侧轴对齐方式，覆盖align-content、align-items效果

### 居中对齐

> 两种方式最好不要混用，IE不兼容，可能会造成居中样式无效

- 容器内元素水平垂直居中，文本也可以

  ```css
  .in_center {
      /*弹性布局*/
      display: flex;
      /*定义容器内的元素垂直居中, 只对单行生效*/
      align-items: center;
      /*定义容器内的元素垂直居中，只对多行生效*/
      align-content: center;
      /*定义容器内的元素水平居中*/
      justify-content: center;
  }
  ```

- 设置元素相对父容器垂直居中

  > 父容器
  >
  > ```css
  > display: flex; /*弹性布局*/
  > ```
  >
  > 子元素
  >
  > ```css
  > margin: auto;
  > ```

## 元素尺寸

### 匹配视窗大小

```css
width: 100vw;
height: 100vh;
```

## 过度 transition

> 效果：如果设定了某属性（该属性一定要设置初始值，例如width不能默认）的过度效果，那么当该属性发生改变时，就以设定的过渡效果过度
>
> | [transition-property](https://www.w3school.com.cn/cssref/pr_transition-property.asp) | 规定设置过渡效果的 CSS 属性的名称。 |
> | ------------------------------------------------------------ | ----------------------------------- |
> | [transition-duration](https://www.w3school.com.cn/cssref/pr_transition-duration.asp) | 规定完成过渡效果需要多少秒或毫秒。  |
> | [transition-timing-function](https://www.w3school.com.cn/cssref/pr_transition-timing-function.asp) | 规定速度效果的速度曲线。            |
> | [transition-delay](https://www.w3school.com.cn/cssref/pr_transition-delay.asp) | 定义过渡效果何时开始。              |

```css
transition: property duration timing-function delay;
transition: width 2s linear 0s;/*宽度发生改变时，均速变化，用时2s，改变发生0s后执行*/
```

## 转换 transform

> 效果：指的是改变所在元素的外观，它有很多种手段(*转换函数*)来改变外观，例如 **位移、缩放、旋转** 等，而其中的位移的函数名就叫`translate`，所以说，`translate`是`transform`的一部分。
>
> [transition transform区别](https://www.jianshu.com/p/80f6051389bd) 
>
> |       函数        |   作用   |                           参数介绍                           |  参数默认值  |
> | :---------------: | :------: | :----------------------------------------------------------: | :----------: |
> | `translate(x, y)` | 元素位移 |                元素偏移的x轴和y轴距离，可为负                | `(0px, 0px)` |
> |   `scale(x, y)`   | 元素缩放 | 元素x轴和y轴缩放的倍数，小于1为缩小，大于1位放大，小于0效果和为0时相等 |   `(1, 1)`   |
> |  `rotate(angle)`  | 元素旋转 |              旋转的角度，单位`deg`，顺时针旋转               |   `(0deg)`   |

## 动画

> [CSS 动画 (w3school.com.cn)](https://www.w3school.com.cn/css/css3_animations.asp) 

### 定义动画

```css
/* 动画中使用transform属性无效，transform属性请配合transition使用，可以实现一定的动画效果 */
@keyframes animationName {
    0%   {background-color:red; left:0px; top:0px;}
    25%  {background-color:yellow; left:200px; top:0px;}
    50%  {background-color:blue; left:200px; top:200px;}
    75%  {background-color:green; left:0px; top:200px;}
    100% {background-color:red; left:0px; top:0px;}
}
```

### 使用动画

```CSS
.className {
    animation-name: animationName; /* 指定使用的动画 */
    animation-duration: 1s; /* 动画时长 */
    animation-delay: 2s; /* 动画开始延迟时间，允许负值（表示已执行的时间） */
    animation-iteration-count: 10; /* 动画执行的次数，infinite表示无限循环 */
    animation-timing-function: linear; /* 动画播放的时间曲线函数 */
    animation-direction: normal; /* 动画播放的方向。normal：向前播放（默认）；reverse：向后播放；alternate：先前再后；alternate-	reverse：先后在前 */
}
```

## 设置不可点击

```css
pointer-events: none;
```

## 定位

### 相对父容器定位

```css
position: relative; /*父容器设置该属性*/
position: absolute; /*子元素设置该属性即可相对父容器定位*/
```

## 为一个元素设置悬浮弹窗

> 设计思路：
>
> - 利用position属性相对父容器进行定位
>
> - 确定目标元素的高宽mw/mh、悬浮窗的宽度xw
>
> - 设置悬浮弹窗为目标元素的兄弟元素并一起放入一个父容器中，然后设置父容器
>
>   ```css
>   poposition: relative; width: max-content;
>   ```
>
>   设置子元素
>
>   ```css
>   poposition: relative; z-index: 2;
>   ```
>
>   设置悬浮弹窗定位在目标元素的正下方
>
>   ```css
>   position: absolute;top: mh+5px;left: -(xw/2-mw/2);z-index: 2;
>   ```
>
> - 若还要设置弹窗幕布，则在新建一个div作为弹窗的兄弟元素，设置
>
>   ```css
>   position: fixed;top: 0px;left: 0px;width: 10000px;height: 10000px;background-color: rgba(0,0,0,0.6);z-index: 1;
>   ```

## 鼠标样式 cursor 

https://blog.csdn.net/wumanxin2018/article/details/77574895

## 背景图片

> 默认情况下，背景图像进行平铺重复显示，以覆盖整个元素实体.
>
> ```css
> background-image:url('gradient2.png');
> ```
>
> 如果想使图片不平铺
>
> ```css
> background-repeat:no-repeat;
> ```
>
> 还可以修改图片在背景中的定位
>
> ```css
> background-position:right top;
> ```
>
> 还可设置图像是否固定或者随着页面的其余部分滚动。
>
> | scroll | 背景图片随着页面的滚动而滚动，这是默认的。 |
> | ------ | ------------------------------------------ |
> | fixed  | 背景图片不会随着页面的滚动而滚动。         |
> | local  | 背景图片会随着元素内容的滚动而滚动。       |
>
> ```css
> background-attachment:fixed;
> ```
>
> 这些属性可以一次性都设置
>
> ```css
> background:#ffffff url('img_tree.png') no-repeat scroll right top;
> ```
>
> 设置背景图片大小需要用到
>
> ```css
> background-size:100% 100%;
> ```

### 固定背景图片全显示

```css
background: url('../image/background-img-2.png') #fcfcf5 no-repeat top center fixed;
background-size: 100%;
```

## 修改svg图标的颜色

> 不是color属性而是fill属性

## 使svg元素居中显示

```css
    display: inline-block;
    vertical-align: middle;
    align-self: center;
```

```html
style="width: 24px;height: 17px;vertical-align: middle;align-self: center;"
```

### css 点击获取ul li 中的值

参考 https://www.cnblogs.com/yangzailu/p/10860759.html

```
let text = $(this).text(); 获取文本
let value = $(this).attr("value"); 获取value
```

### css 超出宽度则显示... 能悬浮显示所有内容

```
1.设置元素宽度，当超过这个宽度就显示.. title悬浮显示所有内容
.xxd1{
white-space: nowrap;
text-overflow: ellipsis;
overflow: hidden;
cursor: pointer;
}
<td width="10%"><div style="width: 85px" title="${l.acctName}" class="xxd1">${l.acctName}</div></td>
```

