---
layout: drafts
title: 枚举类理解
categories: 
- 阅读笔记
tags: 
- Java基础
date: 2021-03-05 09:12:05
---

Java中枚举类型怎么理解
# 认识
**同Object类**


Java中类用关键字class定义，定义后需要实例化成对象再使用时，class类默认都继承自Object类。
**枚举类是用关键字enum定义，类都继承自Enum类。但是实例化的时间和正常类不同，枚举类在定义时候就实例化了对象。**

<!--more-->

下面的代码段定义Direction类的时候初始化了4个Direction的对象
（FONT,BEHIND,LEFT,RIGHT 都是Direction的对象）。
<!--more-->

```java
public enum Direction {

    /*
      在枚举常量后面必须添加分号，因为在枚举常量后面还有其他成员时，分号是必须的。
      枚举常量必须在枚举类中所有成员的上方声明。
    */
    FRONT, BEHIND, LEFT, RIGHT;
}
```

```java 
Direction d = Direction.FRONT;
```
**枚举类主要用于表示有限固定的对象**，如word文档的对齐方式有几种：左对齐、居中对齐、右对齐。开车的方向有几种：前、后、左、右！

# 变量和方法
上例中FRONT, BEHIND, LEFT, RIGHT 都是Direction类的对象，注意，只是对象。那么我们可以在Direction中定义成员变量，实例方法，静态方法等等，
和正常类是一样的，这些方法是对象都可以用的，**枚举类中的方法和属性是对象公用的**。


枚举类也有构造函数，默认都是private修饰，因为枚举类实例不能让外界创建。
创建枚举项就等同于调用本类的无参构造函数，FRONT、BEHIND、LEFT、RIGHT四个枚举项等同于调用了四次无参构造器，所以下例你会看到四个hello输出。
```java 
enum Direction {
    FRONT, BEHIND, LEFT, RIGHT
    /* 
      枚举类的构造器不可以添加访问修饰符，枚举类的构造器默认是private的。
      但你自己不能添加private来修饰构造器。
    */ 
    Direction() {
        System.out.println("hello");
    }
}
```
**枚举类都是Enum的子类**

所有枚举类都是Enum类的子类，同Object一样，我们不需要使用extends来表示继承Enum类。
Enum类结构如下：

![](https://ftp.bmp.ovh/imgs/2021/03/85c497dcd6e3943b.png)

![](https://ftp.bmp.ovh/imgs/2021/03/98ff6549b1e08462.png)

Enum是一个抽象类，定义了name和ordinal两个成员变量，
- name是枚举类实例化名字
- ordinal是枚举实例的序号，在compareTo方法被用于比较计算。

常用方法
- compareTo(E) 枚举类声明的顺序，靠前的小于后面的
- equals 比较两个实例常量是否相当
- static valueOf() 将字符串转换成枚举常量
- static values() 获取枚举对象数组

枚举类中也可以定义抽象类
```java 
enum Direction {
    FRONT() {
        public void fun() {
            System.out.println("FROND：重写了fun()方法");
        }
    }, 
    BEHIND() {
        public void fun() {
            System.out.println("BEHIND：重写了fun()方法");
        }
    }, 
    LEFT() {
        public void fun() {
            System.out.println("LEFT：重写了fun()方法");
        }
    },
    RIGHT() {
        public void fun() {
            System.out.println("RIGHT：重写了fun()方法");
        }
    };
    
    public abstract void fun()[只需要把fun()方法修改为抽象方法，但不可以把Direction类声明为抽象类。];
}
```
# 使用问题
枚举类中实例常量是类的对象，switch语句块中不需要按照类名.常量名，
如下，case 后面跟直接跟FRONT, 而不是Direction.FRONT。

```javascript
        Direction d = Direction.FRONT;
        switch(d) {
            case FRONT: System.out.println("前面");break;
            case BEHIND:System.out.println("后面");break;
            case LEFT:  System.out.println("左面");break;
            case RIGHT: System.out.println("右面");break;
            default:System.out.println("错误的方向");
        }
        Direction d1 = d;
        System.out.println(d1);
```

> 有参考以下博客：
https://www.jianshu.com/p/7d3e3f6695a5
