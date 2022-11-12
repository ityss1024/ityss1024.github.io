

<h1 align="center">1.DOM</h1>

**当网页被加载时，浏览器会创建页面的文档对象模型（Document Object Model）。**

## 1.1 定义

**什么是 DOM？**

DOM 是一项 W3C (World Wide Web Consortium) 标准。

DOM 定义了访问文档的标准：

> “W3C 文档对象模型（DOM）是中立于平台和语言的接口，它允许程序和脚本动态地访问、更新文档的内容、结构和样式。”

W3C DOM 标准被分为 3 个不同的部分：

- Core DOM - 所有文档类型的标准模型
- XML DOM - XML 文档的标准模型
- HTML DOM - HTML 文档的标准模型

**什么是 HTML DOM？**

HTML DOM 是 HTML 的标准*对象*模型和*编程接口*。它定义了：

- 作为*对象*的 HTML 元素
- 所有 HTML 元素的*属性*
- 访问所有 HTML 元素的*方法*
- 所有 HTML 元素的*事件*

**换言之：HTML DOM 是关于如何获取、更改、添加或删除 HTML 元素的标准**。

**DOM 编程界面**

HTML DOM 能够通过 JavaScript 进行访问（也可以通过其他编程语言）。

在 DOM 中，所有 HTML 元素都被定义为*对象*。

编程界面是每个对象的属性和方法。

**属性**是您能够获取或设置的值（就比如改变 HTML 元素的内容）。

**方法**是您能够完成的动作（比如添加或删除 HTML 元素）。

## 1.2 常见属性和方法

**查找 HTML 元素**

| 方法                                    | 描述                   |
| :-------------------------------------- | :--------------------- |
| document.getElementById(*id*)           | 通过元素 id 来查找元素 |
| document.getElementsByTagName(*name*)   | 通过标签名来查找元素   |
| document.getElementsByClassName(*name*) | 通过类名来查找元素     |

**改变 HTML 元素**

| 方法                                       | 描述                   |
| :----------------------------------------- | :--------------------- |
| element.innerHTML = *new html content*     | 改变元素的 inner HTML  |
| element.attribute = *new value*            | 改变 HTML 元素的属性值 |
| element.setAttribute(*attribute*, *value*) | 改变 HTML 元素的属性值 |
| element.style.property = *new style*       | 改变 HTML 元素的样式   |

**添加和删除元素**

| 方法                              | 描述             |
| :-------------------------------- | :--------------- |
| document.createElement(*element*) | 创建 HTML 元素   |
| document.removeChild(*element*)   | 删除 HTML 元素   |
| document.appendChild(*element*)   | 添加 HTML 元素   |
| document.replaceChild(*element*)  | 替换 HTML 元素   |
| document.write(*text*)            | 写入 HTML 输出流 |

**添加事件处理程序**

| 方法                                                     | 描述                            |
| :------------------------------------------------------- | :------------------------------ |
| document.getElementById(id).onclick = function(){*code*} | 向 onclick 事件添加事件处理程序 |



<h1 align="center">2.BOM</h1>

**浏览器对象模型（Browser Object Model (BOM)）允许 JavaScript 与浏览器对话。**

## Window 对象

所有浏览器都支持 *window* 对象。它代表浏览器的窗口。

所有全局 JavaScript 对象，函数和变量自动成为 window 对象的成员。

全局变量是 window 对象的属性。

全局函数是 window 对象的方法。

## Window Location

## Window Location

*window.location* 对象可不带 window 前缀书写。

一些例子：

- window.location.href 返回当前页面的 href (URL)
- window.location.hostname 返回 web 主机的域名
- window.location.pathname 返回当前页面的路径或文件名
- window.location.protocol 返回使用的 web 协议（http: 或 https:）
- window.location.assign 加载新文档

## Window History

window.history 对象可不带 window 书写。

### 一些方法：

- history.back() - 等同于在浏览器点击后退按钮
- history.forward() - 等同于在浏览器中点击前进按钮

**JavaScript Cookies**

参考 https://www.w3school.com.cn/js/js_cookies.asp

