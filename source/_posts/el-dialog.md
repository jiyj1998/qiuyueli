---
layout: drafts
title: el-dialog 使用笔记
categories: 
- 问题笔记
tags:
- vue
date: 2021-04-07 09:12:05
---

# 作用

在保留当前页面状态的情况下，告知用户并承载相关操作。

# 基本内容

dialog内容可以是任意组件

visible属性：控制是否显示（boolean）
title属性 定义标题，默认为空
center属性：为true时可使标题和底部居中，内容不居中

内容分为 ****body**** 和 ****footer**** 两部分， footer内容可以使用slot="footer" 指定。
before-close 属性指定关闭前的操作。

> before-close 仅当用户通过点击关闭图标或遮罩关闭 Dialog 时起效。如果你在 footer 具名 slot 里添加了用于关闭 Dialog 的按钮，那么可以在按钮的点击回调函数里加入 before-close 的相关逻辑。


# 嵌套的Dialog场景
<!-- more -->
这里单独一个标题，是因为嵌套dialog时候有遮罩层级错乱的问题（弹窗前有遮罩效果）
正常情况下，我们不建议使用嵌套的 Dialog，如果需要在页面上同时显示多个 Dialog，可以将它们平级放置。对于确实需要嵌套 Dialog 的场景，我们提供了append-to-body属性。将内层 Dialog 的该属性设置为 true，它就会插入至 body 元素上，从而保证内外层 Dialog 和遮罩层级关系的正确。


# 可能暂时理解不了的

>Dialog 的内容是懒渲染的，即在第一次被打开之前，传入的默认 slot 不会被渲染到 DOM 上。因此，如果需要执行 DOM 操作，或通过 ref 获取相应组件，请在 open 事件回调中进行。

>如果 visible 属性绑定的变量位于 Vuex 的 store 内，那么 .sync 不会正常工作。此时需要去除 .sync 修饰符，同时监听 Dialog 的 open 和 close 事件，在事件回调中执行 Vuex 中对应的 mutation 更新 visible 属性绑定的变量的值。


其他相关属性可查询[官网说明](https://element.eleme.cn/#/zh-CN/component/dialog)

# 问题: width=80% 不起作用
在一个浮动div上调用弹窗的时候发现width 不起作用，一直是默认值50%，我晚上试了很多次，早上吃了很多次，排除了width拼写正确的情况下，我将官网上的样例代码修改了居然成功，真狗

