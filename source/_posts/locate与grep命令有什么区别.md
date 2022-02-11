---
title: locate与grep命令有什么区别
tags:
---

grep 查找的是文件内容
locate 查找的是文件名字，和find 一样，与find的区别是，locate 查找途径是自己的数据库，find 是从硬盘上找，所以locate的速度比find 快。
一般locate的文件数据库在 /var/lib/slocate/slocate.db， 系统会自动维护数据库，也可以手动更新，命令为
```
updatedb
```