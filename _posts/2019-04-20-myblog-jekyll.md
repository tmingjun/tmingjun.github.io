---
title: "我的github博客搭建过程"
athor: xiaotan
data: 2019-04-20
layout: post
description: "记录我搭建自己博客的过程和遇到的问题，由于对前端了解甚少，在jekyll环境的搭建出了很多问题，在各种论坛上找解决方法，最后算是解决了，记录下来。"
tag: jekyll
tag: json
---

>记录我搭建自己博客的过程和遇到的问题，由于对前端了解甚少，在jekyll环境的搭建出了很多问题，在各种论坛上找解决方法，最后算是解决了，记录下来。

## jekyll 本地环境的搭建
由于对 jekyll 的官方文档已经把 jekyll 的安装过程讲解的很详细，步骤如下:

>安装 jekyll 的 ruby 依赖（我用的是deepin系统）:
```
sudo apt-get install ruby-full build-essential
```
>避免用 root 用户安装
```
echo '# Install Ruby Gems to ~/gems' >> ~/.bashrc
echo 'export GEM_HOME="$HOME/gems"' >> ~/.bashrc
echo 'export PATH="$HOME/gems/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc
```
>最后就可以直接安装 jekyll 了：
```
gem install jekyll bundler
```
>在安装jekyll的时候会出问题，提示报错，由于在国内获取源失败了，所以可以通过更新 ruby 源:
```
gem sources --remove https://rubygems.org/
gem sources --add https://gems.ruby-china.com/
```

>jekyll 环境搭建好之后就可以直接开始使用了：

创建一个jekyll本地博客 ```jekyll new youblog```

运行博客：```jekyll s``` 或者 ```jekyll servers```

有时候运行的时候可能会出现没有依赖的问题：
>Dependency Error: Yikes! It looks like you don’t have jekyll-paginate or one of its dependencies installed. In order to use Jekyll as currently configured, you’ll need to install this gem. The full error message from Ruby is: ‘cannot load such file – jekyll-paginate’ If you run into trouble, you can find helpful resources at Getting Help
>jekyll 3.1.2 | Error: jekyll-paginate

解决办法：```gem install jekyll-paginate```, 然后再添加 Gemfile 文件里面添加 ```gem 'jekyll-paginate'```

类似的其他依赖也是一样的安装方法

详情请看:[ jekyll 官方文档](https://www.jekyll.com.cn/docs/)

## 使用别人的博客主题
几个寻找博客主题的网址：
- [jekyll主题1](http://jekyllthemes.org/)
- [jekyll主题2](http://themes.jekyllrc.org/)
- [20个主题](https://www.wowthemes.net/jekyll-themes-templates/)