---
title: "express_api"
date: 2020-7-25T22:53:28+08:00
tags: ["nodejs", "express"]
categories: ["js"]
---
## Express API 总结
#### 先来个基本操作
```js
const express = require('express');
let app = express();

app.get('/', function(req, res) {
  res.send('hello world');
});

let server = app.listen(3000, function() {
  let host = server.address().address;
  let port = server.address().port;

  console.log(`app listening at port: ${port}`);
});
```
### express.xxx - 内置中间件
#### json([option])
内置中间件,解析传入的请求
```js
app.use(express.json())
app.use((request, response, next) => {
    const jsonObj = request.body 
})
```
#### static(root，[option])
内置中间件为，创建一个静态文件服务器，根据 req.url 来寻找对应的文件
#### text([option])
内置中间件，将传入的请求参数解析为字符串
#### Router([option])
创建一个 router 对象，对路由进行响应
### app.xxx - 应用设置
#### app.set(name , value)
存储一个变量
#### app.use([path, ] callback [, callback])
使用中间件进行全局的处理
对应的路由进行响应

### router.xxx - 操作路由
```js
var app = express();
var router = express.Router();

//  没有挂载路径的中间件，通过该路由的每个请求都会执行该中间件
router.use(function(req, res, next) {
  console.log('Time:', Date.now());
  next();
});

//  一个中间件栈，显示任何指向/user/:id的HTTP请求信息
router.use('/user/:id', function(req, res, next) {
  console.log('Request URL:', req.originUrl);
  next();
}, function(req, res, next) {
  console.log('Request Type:', req.method);
  next();
});

//  一个中间件栈，处理指向/user/:id的GET请求
router.get('/user/:id', function(req, res, next) {
  //  如果user id为0，跳到下一个路由
  if(req.params.id == 0)  next('route');
  //  负责将控制权交给栈中下一个中间件
  else next();
}, function(req, res, next) {
  //  渲染常规页面
  res.render('regular');
});

//  处理/user/:id，渲染一个特殊页面
router.get('/user/:id', function(req, res, next) {
  console.log(req.params.id);
  res.render('special');
});

//  将路由挂载至应用
app.use('/', router);
```
#### router.all(path, [callback, ... ] callback)
与 methods 相同，适配所有的方法
#### router.methods(path, fn)
get/post/put/delete/update 对应的请求方法进行响应
#### router.param(name, callback)
构造一个参数触发器，根据参数出发回调
即使参数在多个路由中匹配，在请求-响应周期中也仅会调用一次参数回调
#### router.use([path], [function], funtion)
中间件的使用或者对路由的响应
#### router.route(path)
返回单个路由的实例，然后您可以使用该路由使用可选的中间件来处理HTTP动词。使用router.route()以避免重复请求的响应

### 错误处理
```js
var bodyParser = require('body-Parser');
var methodOverride = require('method-override');

app.use(bodyParser());
app.use(methodOverride());
app.use(function(err, req, res, next) {
  //  业务逻辑
  console.error(err.stack);
  res.status(500).send('Something broke!');
});
```