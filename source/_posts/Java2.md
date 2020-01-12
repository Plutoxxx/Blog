---
title: Java基础②
<!-- img: https://image-1300514593.cos.ap-shanghai.myqcloud.com/featureimages/3.jpg -->
top: false
cover: false
toc: true
mathjax: true
date: 2019-11-03 14:53:35
password:
summary: 总结Java中集合相关的知识🤣。
tags:
- Java
- 语言
categories:
- Java
---
<div align="middle"><iframe frameborder="no" border="0" marginwidth="0" marginheight="0" width=330 height=86 src="//music.163.com/outchain/player?type=2&id=551277612&auto=1&height=66"></iframe></div>

>主要总结Java中集合相关的知识，若有错误，欢迎更正🤣。

# Java集合
---

## collection常用功能

Collection是所有单列集合的父接口，Collection中定义了单列集合（List和Set）通用的一些方法，这些方法可以操作所有的单列集合。方法如下：

* `public boolean add(E e)`: 把给定的对象添加到当前集合中 。
* `public void clear()`: 清空集合中所有的元素。
* `public boolean remove(E e)`: 把给定的对象在当前集合中删除。
* `public boolean contains(E e)`: 判断当前集合中是否包含给定的对象。
* `public boolean isEmpty()`: 判断当前集合是否为空。
* `public int size()`: 返回集合中元素的个数。
* `public Object[] toArray()`: 把集合中的元素，存储到数组中。

## iterator迭代器

### 1. 迭代的概念
* **迭代**：Collection集合元素的通用获取方式。在取出元素之前要先判断集合中有没有元素，如果有，就把这个元素取出来，继续判断，如果还有就再取出来。一直把集合中的所有元素全部取出来。这种取出方式专业术语称为迭代。

### 2. iterator接口的常用方法
* `public E next()`: 返回迭代的下一个元素。
* `public boolean hasNext`: 如果仍有元素可以迭代，则返回true。

### 3. 增强for循环
* 专门用来遍历数组和集合的，内部原理其实是一个Iterator迭代器，所以在遍历的过程中，不能对集合中的元素进行增删操作。格式为：
```java
for(type var : collection集合 or 数组){
	...
}
```

## List

List是Collection集合的子接口，不但继承了Collection接口中的方法，而且增加一些根据元素索引来操作集合的特有方法

### 1. List接口特点
* 它是一个元素存取有序的集合。
* 它是一个带有索引的集合，通过索引就可以精确操作集合中的元素
* 集合中可以有重复的元素，通过元素的equals方法，来比较是否为重复的元素

### 2. List接口中常用方法
- `public void add(int index, E element)`： 将指定的元素，添加到该集合中的指定位置上。
- `public E get(int index)`：返回集合中指定位置的元素。
- `public E remove(int index)`: 移除列表中指定位置的元素, 返回的是被移除的元素。
- `public E set(int index, E element)`：用指定元素替换集合中指定位置的元素,返回值的更新前的元素。

### 3. ArrayList集合（List子类）
* 数据存储的格式是数组结构。元素增删慢，查找快。

### 4. LinkList集合（List子类）
* 数据存储的结构是链表结构。元素增删快，查询慢。
* 里边包含了大量操作首尾元素的方法。
- `public void addFirst(E e)`：将指定元素插入此列表的开头。
- `public void addLast(E e)`：将指定元素添加到此列表的结尾。
- `public void push(E e)`：将元素推入此列表所表示的堆栈。
- `public E getFirst()`：返回此列表的第一个元素。
- `public E getLast()`：返回此列表的最后一个元素。
- `public E removeFirst()`：移除并返回此列表的第一个元素。
- `public E removeLast()`：移除并返回此列表的最后一个元素。
- `public E pop()`:从此列表所表示的堆栈处弹出一个元素。
- `public boolean isEmpty()`：如果列表不包含元素，则返回true。

>tips：使用LinkedList集合特有的方法,不能使用多态。


## Set

同样继承自Collection接口，与Collection接口中的方法基本一致。
### 1. Set接口特点
* 不允许存储重复的元素。
* 没有索引，没有带索引的方法，也不能用普通的for循环遍历。

### 2. HashSet（Set实现）
* 根据对象的哈希值来确定元素在集合中的存储位置，因此具有良好的存取和查找性能。保证元素唯一性的方式依赖于hashCode与equals方法。

>tips：必须重写hashCode和equals方法。

### 3. LinkedHashSet（Set实现）
* 数据为链表+哈希表组合的存储结构。
* 元素放入取出是有顺序的。

## 可变参数

当方法参数列表已经确定，但是参数个数不确定时，可以用可变参数。格式为：
```java
修饰符 返回值类型 method_name(type ...var){
	方法体
}
```
> * 一个方法的参数列表，只能有一个参数变量。
* 如果方法的参数有多个，那么可变参数必须写在参数列表末尾。


## Map

### 1. Map集合特点
* Map集合是一个双列集合,一个元素包含两个值(一个key,一个value)。
* Map集合中的元素,key和value的数据类型可以相同,也可以不同。
* Map集合中的元素,key是不允许重复的,value是可以重复的。
* Map集合中的元素,key和value是一一对应。

### 2. HsahMap（Map实现）
* HashMap集合底层是哈希表:查询的速度特别的快。
* hashMap集合是一个无序的集合,存储元素和取出元素的顺序有可能不一致。

### 3. LinkedHashMap（HsahMap实现）
* LinkedHashMap集合底层是哈希表+链表(保证迭代的顺序)。
* LinkedHashMap集合是一个有序的集合,存储元素和取出元素的顺序是一致的。

## JDK9新特性
List、Set、Map接口:里边增加了一个静态的方法of,可以给集合一次性添加多个元素。
* `static <E> List<E> of​(E... elements)`：一次性添加多个元素。

> * of方法只适用于List接口，Set接口，Map接口，不适用于接接口的实现类。
* of方法的返回值是一个不能改变的集合，集合不能再使用add，put方法添加元素，否则会抛出异常。
* Set接口和Map接口在调用of方法的时候，不能有重复的元素，否则会抛出异常。