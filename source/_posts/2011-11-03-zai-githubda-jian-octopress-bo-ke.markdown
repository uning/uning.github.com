---
layout: post
title: "如何写blog -- 在github搭建-Octopress 博客"
date: 2011-11-03 14:00
comments: true
categories: 
- Tech
- Blog System
- 博客系统
- Octopress
---
所有工作在Centos 5上完成,参考[官方文档](http://octopress.org/docs/),繁体教程

- ###安装ruby 环境 
  推荐使用 rvm 处理不同ruby 版本在项目间切换
``` bash
  bash < <(curl -s https://raw.github.com/wayneeseguin/rvm/master/binscripts/rvm-installer )
  echo '[[ -s "$HOME/.rvm/scripts/rvm" ]] && . "$HOME/.rvm/scripts/rvm" # Load RVM function' >>$HOME/.bash_profile
  source ~/.bash_profile 
  type rvm | head -1  #验证rvm 安装 output: rvm is a function
  rvm install 1.9.2 && rvm use 1.9.2  #安装ruby 1.9.2
```
- ###下载octopress
``` bash
  git clone git://github.com/imathis/octopress.git
  cd octopress/
  gem install bundle #安装依赖
  bundle install    
  rake install    #安装theme
```
- ###设置部署环境，这里跟github-pages 整合
```
  rake setup_github_pages #会提示输入git库地址，现在github 上创建项目 {youid}.github.com, 地址是git@github.com:{youid}/{youid}.github.com , 如果要deploy，需要将本机.ssh/id_rsa.pub 放到github里去
  rake generate
  rake deploy
```

- ###编写blog
``` bash
    rake new_post["在github搭建-Octopress 博客"]

    rake generate   #生成内容
    rake preview    #可以在 4000端口 预览生成的内容
```
- ###在octopress 设置github源码提交
  打开 .git/config添加
```
[remote "origin"]
	url = git@github.com:$youid/$youid.github.com.git
    fetch = +refs/heads/*:refs/remotes/origin/*
[branch "source"]
	remote = origin
	merge = refs/heads/source
```
  执行
``` bash
  git commit -am'prepare for source commit'
  git branch source
  git push origin source
```
--------------------------------------------------
##问题&解决
   code 插件pyments 高亮问题
``` bash 
   .rvm/gems/ruby-1.9.2-p290/gems/ffi-1.0.10/lib/ffi/library.rb:121:in `block in ffi_lib': Could not open library 'lib.so': lib.so: cannot open shared object file: No such file or directory (LoadError)
   from /home/hotel/.rvm/gems/ruby-1.9.2-p290/gems/ffi-1.0.10/lib/ffi/library.rb:88:in `map'
   from /home/hotel/.rvm/gems/ruby-1.9.2-p290/gems/ffi-1.0.10/lib/ffi/library.rb:88:in `ffi_lib'
   from /home/hotel/.rvm/gems/ruby-1.9.2-p290/gems/rubypython-0.5.1/lib/rubypython/python.rb:29:in `<module:Python>'
   from /home/hotel/.rvm/gems/ruby-1.9.2-p290/gems/rubypython-0.5.1/lib/rubypython/python.rb:21:in `<top (required)>'
   from /home/hotel/.rvm/gems/ruby-1.9.2-p290/gems/rubypython-0.5.1/lib/rubypython.rb:261:in `load'
   from /home/hotel/.rvm/gems/ruby-1.9.2-p290/gems/rubypython-0.5.1/lib/rubypython.rb:261:in `reload_library'
   from /home/hotel/.rvm/gems/ruby-1.9.2-p290/gems/rubypython-0.5.1/lib/rubypython.rb:104:in `start'
   from /home/hotel/.rvm/gems/ruby-1.9.2-p290/gems/pygments.rb-0.1.3/lib/pygments/ffi.rb:8:in `start'
   from /home/hotel/.rvm/gems/ruby-1.9.2-p290/gems/pygments.rb-0.1.3/lib/pygments/ffi.rb:82:in `highlight'
   from t.rb:4:in `<main>'
```

   将以下两个库链接到lib下即可解决
``` bash 
   sudo ln -s /usr/lib64/libpython2.4.so.1.0 /usr/lib/libpython2.4.so.1.0  #如果是高版本的python ，链接对应版本的库即可
   sudo ln -s /usr/lib64/libpython2.4.so  /usr/lib/libpython2.4.so
``` 






  

