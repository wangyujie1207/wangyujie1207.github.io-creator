---
title: "记录一下hugo搭建博客的经历"
date: 2019-10-26T11:03:42+08:00
draft: false
---

# 安装hugo, 参考 [hugo搭建](https://gohugo.io/);

```
mac 安装
homebrew install hugo
hugo version
```

# 开始搭建博客
找一个文件夹, hugo new site <网站名>
```
hugo new site quickstart
```
#### 如果需要部署到GitHub, 需要注意一下资源路径

#### GitHub页面有两种类型
* ``https://<USERNAME|ORGANIZATION>.github.io/``
* ``https://<USERNAME|ORGANIZATION>.github.io/<PROJECT>/``

#### 我用的第一种 
```
hugo new site <names>.github.io-creator
```

## 为网站添加一个主题
```
cd <names>
git init
git submodule add https://github.com/budparr/gohugo-theme-ananke.git themes/ananke
echo 'theme = "ananke"' >> config.toml
```

## 新建一篇文章
```
hugo new posts/<names>.md
```
如需要发布文章，记得把draft: true改为draft: false. 参考 [draft](https://gohugo.io/getting-started/usage/#draft-future-and-expired-content)

## 预览网站
```
hugo server -D
```
网站配置文件是config.toml，如可配置语言选项为languageCode = “zh-Hans”,网站名字等

## 生成静态文件
* 这个就很简单啦, 直接运行hugo命令生成静态网页，放在public目录下
```
hugo
```

* 最后, 提交public到GitHub 然后开启gh-pages即可预览