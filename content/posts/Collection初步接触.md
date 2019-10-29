---
title: "Collection初步接触"
date: 2019-10-29T13:53:28+08:00
tags: ["java", "collection"]
categories: ["java"]
---
# Java集合的集成体系
Java的集合类主要由两个接口派生而出：Collection和Map,Collection和Map是Java集合框架的根接口。一张图看出Java collection的重要性

* Collection接口是Set,Queue,List的父接口。Collection接口中定义了多种方法可供其子类进行实现，以实现数据操作。

![](/images/1.png)

### List
list add时,容量看起来无限,实际内部进行了扩容,扩容大小为当前容量的一半

### Set
* 不允许出现重复的元素
* 集合中的元素位置无顺序
* 有且只有一个值为null的元素

因为set是一个抽象的接口，所以不能直接实例化一个set对象。（Set s = new Set()是错误的）

Set接口的两大实现：HashSet、TreeSet

HashSet 是无序的，如果要保持顺序，可以使用LinkedHashSet.

### HashMap和HashSet
* HashSet
    * HashSet实现了Set接口，不允许集合中有重复的值
* HashMap
    * HashMap实现了Map接口，Map接口对键值对进行映射。Map中不允许重复的键
    * Map接口的俩个基本实现：HashMap和TreeMap，TreeMap保存了对象的排列次序，而HashMap则不能。
    * HashMap允许键和值为null

![](/images/2.png)
### Collection中常用的方法
Guava 集合工具类库
```
//添加方法：
add(Object o) //添加指定元素
addAll(Collection c) //添加指定集合
//删除方法：
remove(Object o) //删除指定元素
removeAll(Collection c) //输出两个集合的交集
retainAll(Collection c) //保留两个集合的交集
clear() //清空集合
//查询方法：
size() //集合中的有效元素个数
toArray() //将集合中的元素转换成Object类型数组
//判断方法：
isEmpty() //判断是否为空
equals(Object o) //判断是否与指定元素相同
contains(Object o) //判断是否包含指定元素
containsAll(Collection c) //判断是否包含指定集合
```

### ArrayList中特有的方法

```
ensureCapacity(int minCapactiy) //判断当前数组中的元素个数是否大于指定的minCapacity
trimToSize() //修改数组容量为当前数组有效元素个数
```

### LinkedList中特有的方法

```
//查询方法：
getFirst() //获取集合中的第一个元素
getLast() //获取集合中的最后一个元素
//添加方法：
addFirst(Object o) //在集合的第一个位置添加指定元素
addLast(Object o) //在集合的最后一个位置添加指定元素
//删除方法：
removeFirst() //删除集合中的第一个元素
removeLast() //删除集合中的最后一个元素
```

