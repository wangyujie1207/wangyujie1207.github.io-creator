---
title: "Java多线程"
date: 2019-11-05T13:24:31+08:00
tags: ["java", "多线程"]
categories: ["java"]
---
## 什么是多线程
多线程是指在同一程序中有多个顺序流在执行。

* 什么是线程
* 为什么需要多线程
* Java中的线程表示
* 多线程问题的来源
* 多线程的适用场景

### 同步与异步

同步和异步关注的是消息通信机制

* 所谓同步，就是在发出一个调用时，会一直等待调用的返回结果。
* 而异步则是相反，调用在发出之后，这个调用就直接返回了，所以没有返回结果。换句话说，当一个异步过程调用发出后，调用者不会立刻得到结果。而是在调用发出后，被调用者通过状态、通知来通知调用者，或通过回调函数处理这个调用。

### 阻塞与非阻塞
阻塞和非阻塞关注的是程序在等待调用结果（消息，返回值）时的状态.

* 阻塞调用是指调用结果返回之前，当前线程会被挂起。调用线程只有在得到结果之后才会返回。
* 非阻塞调用指在不能立刻得到结果之前，该调用不会阻塞当前线程。

## 为什么需要多线程
* 因为java的执行模型：最初是同步/阻塞的，且默认情况下只有一个线程，但是事件太多会导致等待时间过长或当线程被挂起会导致后面的事务无法进行，因此需要多线程。
* CPU快，现代CPU都是多核，因此可以通过多线程来提高性能问题

``` javascript
CPU进程的时间：由操作系统决定CPU每一个进程每一个线程可以占据多少时间，如果超时，CPU会强制让它终止去执行下一个。
```

## Java中的线程表示

### Thread

* Java中只有这么⼀种东⻄代表线程
* start⽅法才能并发执⾏！
    * start方法执行，无需等待
    * run方法执行，等待完成再做下件事情，必须要start，不然创建了线程也没有并行执行
    * 新的线程入口是run
* 每多开⼀个线程，就多⼀个执⾏流
* 多线程执行时是乱序的
* ⽅法栈(局部变量)是线程私有的
* 静态变量/类变量是被所有线程共享的

### 多线程带来的问题

```html
多线程的难点是，变量被所有线程共享时候，可能会出问题，譬如多线程执行i++，因为i++不是原子操作。
一段代码可能同时有多个线程执行，是问题的来源。如线程1和线程2共同执行i++，因为变量不是原子的，将i写回时可能导致值就出问题了
```

### 多线程的生命周期

![](/images/thread.png)

### 多线程使用的目的

* 吞吐量：做WEB，容器帮你做了多线程，但是它只能帮你做请求层面的，简单的说，就是一个请求一个线程(如struts2，是多线程的，每个客户端请求创建一个实例，保证线程安全)，或多个请求一个线程，如果是单线程，那只能是处理一个用户的请求
* 伸缩性：通过增加CPU核数来提升性能。

### 多线程的适用场景

* 常见的浏览器、Web服务(现在写的web是中间件帮你完成了线程的控制)，web处理请求，各种专用服务器(如游戏服务器)
* servlet多线程
* FTP下载，多线程操作文件
* 数据库用到的多线程
* 分布式计算
* tomcat，tomcat内部采用多线程，上百个客户端访问同一个WEB应用，tomcat接入后就是把后续的处理扔给一个新的线程来处理，这个新的线程最后调用我们的servlet程序，比如doGet或者dpPost方法
* 后台任务：如定时向大量(100W以上)的用户发送邮件；定期更新配置文件、任务调度(如quartz)，一些监控用于定期信息采集
* 自动作业处理：比如定期备份日志、定期备份数据库
* 异步处理：如发微博、记录日志
* 页面异步处理：比如大批量数据的核对工作(有10万个手机号码，核对哪些是已有用户)
* 数据库的数据分析(待分析的数据太多)，数据迁移
* 多步骤的任务处理，可根据步骤特征选用不同个数和特征的线程来协作处理，多任务的分割，由一个主线程分割给多个线程完成
* desktop应用开发，一个费时的计算开个线程，前台加个进度条显示
* swing编程

