---
layout: article
title: computed 和 watch 的区别和运用的场景
mathjax: true
---




computed 是计算属性，依赖其它属性计算值，并且 computed 的值有缓存，职友集当计算值变化才会返回内容，他可以设置getter和setter。

watch 监听到值的变化就会执行回调，在回调中可以进行一系列的操作。

计算属性一般用在模板渲染中，某个值是依赖其它响应对象甚至是计算属性而来；而侦听属性适用于观测某个值的变化去完成一段复杂的业务逻辑。
