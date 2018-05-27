---
title: Mac OS X 基于hexo搭建自己的博客
date: 2018-05-27 14:21:06
tags:
---
Hexo 是一个快速、简洁且高效的博客框架。Hexo 使用 Markdown（或其他渲染引擎）解析文章，在几秒内，即可利用靓丽的主题生成静态网页。
更多查看： https://hexo.io/zh-cn/docs/

#### 一、安装hexo
<pre><code>
sudo npm install -g hexo
</code>
#### 二、创建文件夹
<pre><code>
mkdir firstBlog
cd firstBlog
hexo init
</code>

之后得到如下目录
<pre><code>
·
|-- _config.yml
|-- package-lock.json
|-- package.json
|-- scaffolds
|-- source
|   |-- _posts
|-- themes
</code>
#### 三、生成静态网页
<pre><code>
hexo generate
</code>
#### 四、在服务器上运行
<pre><code> 
hexo server

假如你想指定端口可以使用下面命令
hexo server -p 端口号
或者 hexo s -p 端口号
</code>
#### 五、撰写博客
<pre><code> 
hexo new post “博客名字”
</code>
成功后出现
<pre><code> 
INFO  Created: ~/Desktop/博客/firstBlog/source/_posts/’博客名字‘.md
</code>

#### 问题小结
``` yaml
安装 直接使用 npm install -g hexo 会出现权限错误
```

``` yaml
我是克隆github上面已经建好的博客目录，启动端口，出现空白界面 终端出现提示 : WARN No layout: index.html
这个问题主要出在主题上面 
1.检查在themes文件夹下是否存在主题文件。
2.检查在themes文件夹的主题名字 与根目录_config.yml 配置的主题名字是否一致
```


