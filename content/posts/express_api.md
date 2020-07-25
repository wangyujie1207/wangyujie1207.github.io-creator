---
title: "express_api"
date: 2019-10-29T13:53:28+08:00
tags: ["nodejs", "express"]
categories: ["js"]
---
## Express API 总结
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
#### router.all(path, [callback, ... ] callback)
与 methods 相同，适配所有的方法
#### router.methods(path, fn)
get/post/put/delete/update 对应的请求方法进行响应
#### router.param(name, callback)
构造一个参数触发器，根据参数出发回调
即使参数在多个路由中匹配，在请求-响应周期中也仅会调用一次参数回调
```js
router.param('id', function (req, res, next, id) {
  console.log('CALLED ONLY ONCE')
  next()
})

router.get('/user/:id', function (req, res, next) {
  console.log('although this matches')
  next()
})

router.get('/user/:id', function (req, res) {
  console.log('and this matches too')
  res.end()
})
/*print
CALLED ONLY ONCE
although this matches
and this matches too
*/
```
#### router.use([path], [function], funtion)
中间件的使用或者对路由的响应
#### router.route(path)
返回单个路由的实例，然后您可以使用该路由使用可选的中间件来处理HTTP动词。使用router.route()以避免重复请求的响应
```js
router.route('/users/:user_id')
  .all(function (req, res, next) {
    // runs for all HTTP verbs first
    // think of it as route specific middleware!
    next()
  })
  .get(function (req, res, next) {
    res.json(req.user)
  })
  .post(function (req, res, next) {
    next(new Error('not implemented'))
  })
  .delete(function (req, res, next) {
    next(new Error('not implemented'))
  })
```