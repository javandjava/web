---
title: Java基本知识
excerpt: Java的一些简单知识
date: 2021-11-22 10:52:07
tags: Java
categories: Java
---



## HashMap

1. 底层实现：数组+链表/红黑树(链表超过8个，转为红黑树)



## Lambda

1. 本质：匿名函数
2. 组成：参数列表，->，函数体，函数体可以是表达式也可以是语句块
3. Example

```java
List<Player> players
for (Player p:players){
	System.out.print(p)
}

players.forEach(p->System.out.println(p))
players.forEach(System.out::println)
```



## JDK8 新特性

1. 时间函数
2. Predicate
3. Function
