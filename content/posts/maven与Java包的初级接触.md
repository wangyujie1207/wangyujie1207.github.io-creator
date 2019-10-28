---
title: "Maven与Java包的初级接触"
date: 2019-10-28T13:46:32+08:00
tags: ["java", "maven"]
categories: ["java"]
---

# 什么是maven
    Maven是一个采用纯Java编写的开源项目管理工具, Maven采用了一种被称之为
    Project Object Model (POM)概念来管理项目，所有的项目配置信息都被定
    义在一个叫做POM.xml的文件中..
* Maven主要服务于基于Java平台的项目构建、依赖管理和项目信息管理...

# 仓库
## 本地仓库
* Maven会把我们项目所构建出来的jar包等等资源存放在本地仓库中。当我们需要jar包的时候，Maven第一时间也是去本地仓库中寻找jar包
## 中心仓库
* ** 当Maven在本地仓库和私服找不到我们需要的jar包的时候，就去中心仓库中帮我们下载对应的jar包**。那Maven怎么知道去哪里下载呢？？其实Maven已经配置好的了
apache-maven-3.2.1\lib\maven-model-builder-3.2.1\org\apache\maven\model下的POM.xml文件中已经配置好了

## maven坐标
#### 坐标的组成： groupId + artifactId+ version

```
* groupId：组id ,机构名，公司名：好比公司的id，或者是公司包名 alibaba ——-》高德--》5.01版本
* artifactId：构建物id ，产品名或者产品的id
* version ：版本号
```

#### jar包组成： artifactId-version.jar

scope应用范围有test、compile等等，默认是compile，那么test和compile有什么区别呢？

* 间接依赖问题 ：依赖的jar包必须是 compile 范围，假如是test范围，则发布的jar包不会包含test范围依赖的jar包，和依赖关系

```xml
<scope>test</scope>
```

# Java的包管理机制
##. 什么是包
* JVM的工作被设计得相当简单：

``` 
1. 执行一个类的字节码
2. 假如这个过程中碰到了新的类，加载他
```
* 那么去哪里加载他呢？

## 类路径（Classpath）
* 什么是类路径：-classpath/-cp
* 类的全限定类名（目录层级）唯一确定了一个类
* 包就是把许多类放在一起打的压缩包

## Classpath hell
* 传递性依赖是指你依赖的类还依赖了别的类
* 全限定类名是类的唯一标识
* 当多个同名类同时出现在Classpath中，就是噩梦的开始

## 什么是包管理
* 你要使用一些第三方类，就要告诉JVM从哪里找
* 包管理的实质就是告诉JVM如何找到所需的第三方库以及成功地解决其中地冲突问题

## Maven——划时代的包管理工具
* 约定优于配置（Convention over configuration）
* 必须强调，Maven远远不止是包管理工具
* Maven的包按照约定为所有的包编号，方便检索，groupId/artifactId/version
* 依赖冲突的解决原则：最近的胜出
* 当你看到如下异常的时候：

```markdown
* AbstractMethodError
* NoClassDefFoundError
* ClassNotFoundException
* LinkageError
```

* 一般就是包冲突了，解决方法：

```markdown
* 单独声明需要引用的特定包
* 排除掉冲突的包
```