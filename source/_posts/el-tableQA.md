---
title: el-table对不齐
categories: 
- 问题笔记
tags: 
- vue
date: 2021-03-30 09:08:29
---
**问题**： el-table 有多列时，除了最后一列外都设置了宽度属性，发现表头行天聪不满边框
<!--more-->
加入了一下样式解决
```css
    /deep/
    .el-table th.gutter{
      display: table-cell!important;
    }
```
