---
layout: post
category: records
tags : [intro, beginner]
title: My Fist Post to GitHub
---
#{{page.title}}

<p class="meta">04 Nov 2012 </p>

  昨天用了接近一天的时间，去了解[github](http://www.github.com)以及git的相关内容。在这么短的时间内，能够了解的毕竟有限，但是也足够让我喜欢上github了。除了他强大的版本控制和分支控制的哲学以外，利用github的pages做一个博客，然后用markdown语言写作，也是一件相当赞的事情。于是，接着上午对github的粗浅了解，下午就开始了折腾github pages的进程。

##GitHub + jekyll
  
 
   在网上查了很多资料，有这几篇，给我的帮助最大：

- BeiYuu所写的[使用GitHub Pages建独立博客](http://beiyuu.com/github-pages/#github)
- 雁起平沙的[GitHub Pages极简教程](http://yanping.me/cn/blog/2012/03/18/github-pages-step-by-step/)
- 阮一峰所写的[搭建一个免费的，无限流量的Blog----github Pages和jekyll入门](http://www.ruanyifeng.com/blog/2012/08/blogging_with_jekyll.html)

对于我这样的菜鸟而言，如果不在本地查看，而是每次都要到github网站上面查看博客效果的话，挺不方便。一来因为对于设计的感觉太差，需要经常调整，如果只能够在网络上查看，每次都要用git add + git commit + git push，特别麻烦。二来，如果连接不上网络的时候（虽然可能性较小），在本地可以继续写作，并随时查看效果，只要等到有网络了，再推送上去即可，丝毫不影响工作进程。
    
当然，如果是高手的话，可以只是安装git(在windows下可安装[mysgit](http://code.google.com/p/msysgit/downloads/list)),而不必安装jekyll和ruby环境(ruby环境在这里只有一个作用：为jekyll提供服务)。

下面开始记录一下我的安装情况，很多地方都是参照上面三篇博文所做的，本文只是记录我个人的使用情形，顺便练习一下markdown语言的用法。

## 一、创建github账号，安装github
    

为了省事，可以在创建github之后，直接下载github提供的[软件](http://www.github.com).只是，似乎github软件不能够自定义安装路径。因为是挺久之前创建的账号和安装的github软件，我记不太清了。只是从我的电脑上面查看，github并没有安装在C盘或D盘的Program files 目录下。

接下来，就需要*创建公钥*了。以windows为例，在C:\Users\user-name\.ssh文件夹中用 cd ~/.ssh进入。如果显示“No such file or directory”，则说明没有key文件，需要自己创建。
   
   如果已经存在ssh key设置（在~/.ssh文件夹中，有id_rsa 和id_rsa.pub两个文件），则需要先将其备份到key_backup文件夹中，然后将.ssh文件夹下的原文件删除。

   好了，现在可以生成新的SSH key文件了：
- $ ssh -keygen -t rsa -C "username@youremail.com"
- Generating public/private rsa key pair.
- Enter file in which to save the key(/Users/your_user_directory/.ssh/id_rsa):

按照默认的设置，按下回车确认即可，不必更改存储key文件的位置。
接下来，系统会要求你输入加密串（Passphrase）。

输入并确认输入之后，就成功设置了ssh key，再次查看.ssh文件夹，即可见到id_rsa（私钥）和id_rsa.pub(公钥)两个文件了。

之后，将id_rsa.pub用文本编辑器（vim，notepad等等均可）打开，拷贝其中全部内容。然后将SSH Key添加到GitHub上去。

在GitHub主页上面（登陆后），点击设置按钮，选择SSH key选项，点击add，然后将复制的内容粘贴到出现的窗体之中，点击“Add key”即可。
   
接下来，测试是否能够成功连接，输入命令：
$ ssh -T git@github.com      # git@github.com为测试的地址，不要更改

如果成功，会显示如下内容：

Hi 'Your name'! You've successfully authenticated, but GitHub dose not provide shell access.

我在设置ssh key 文件的过程中，见到.ssh之中，出现了github_rsa和github_rsa.pub两个文件，但是在使用生成命令之前，没有id_rsa和id_rsa.pub两个文件。没有去理会，有可能是github软件安装的过程之中自动生成了ssh key文件。但是，这些都是可以自己替换的。我按照上面的步骤，将重新生成的id_rsa.pub中的公钥文本粘贴到github网站上面，添加了key。测试成功。至于github_rsa是怎么来的，不很清楚。


##设置github账号信息
   
   在git shell 中使用命令：
$ git config --global user.name  "your names"
$ git config --global user.email "your email"
   
OK,现在github的设置已经完成。接下来就要转到*博客部分*了。
   
从我搭建博客的感觉来看，对于初学者，雁落平沙的“极简教程”是比较合适的，而如果参照阮一峰的教程，则需要对前端有较多的了解，更复杂一点，需要自己去构建符合jekyll要求的文档。
   
   github pages有两种：
- project pages，依附于项目，每个项目只能够有一个pages，建立在gh-pages分支上,创建后，访问的地址为： http://username.github.com/project；
- user pages，新建一个repo，命名为username.github.com，使用master分支。每个用户只能够建立一个，创建成功后，访问的地址为: http://username.github.com.
   
在具体的构建上面，二者大同小异，只是分支不同罢了。我选择了第二种方式创建自己的博客。

## 创建GitHub Pages

- 创建代码库，命名为username.github.com(必须是你在github使用的用户名)
   
- 在线生成pages*， 进入上述仓库，点击“Admin”选项，进入。然后选择Automatic GitHub Page Generator,按照流程提示走下去，创建好页面。
   
- 将代码库克隆至本地：

git clone git@github.com: username/username.github.com.git

删除该目录下的index.html，但不要将.git目录给删除了。

回到存储gitcode的主目录，创建一个other_site，cd 进入，克隆别人的代码库：
git clone git@github.com:mojombo/mojombo.github.com.git

下载后，将.git目录删除，把其他文件复制到自己的本地代码库username.github.com中。

之后，就可以根据需要配置自己的博客了。这里需要对jekyll的架构和作用有个基本的了解。

## jekyll的结构
   
基本结构如下（从beiyuu的博文中copy而来）：   

|-- _config.yml
|-- _includes
|-- _layouts
|   |-- default.html
|   `-- post.html
|-- _posts
|   |-- 2007-10-29-why-every-programmer-should-play-nethack.textile
|   `-- 2009-04-26-barcamp-boston-4-roundup.textile
|-- _site
`-- index.html

- _config.yml为配置文件，定义了全局变量，用于设定想要得到的网站效果，语言解释器的选择等等的内容。一般只需要根据相应的文档设置好了即可。

- includes： 文件夹，类似于编程语言源码之中的include文件夹，用来存放一些可以重用的模块，通过类似{%include example_file.ext%}的语句进行调用。可以用在模板（template）和普通的文件之中。

- layouts: 存储模板文件的位置。一般至少需要两个模板文件：default和posts。
需要通过YAML front matter来定义，在模板文件中的{{content}}标记语句，用来将数据插入到模板中来。在jekyll运行时候，会为你自动做到这些插入。

- posts： 存储博文的文件夹。需要严格遵守这样的方式命名：2012-11-04-first-post.md。md为后缀名，也可以为textile或者html。你要做的主要工作，就是用这些标记语言写作，然后扔到这个文件夹中，不用去管文章的样式，结构，背景等等，jekyll会为你做到这些，前提是你设置好了模板。当然，也可以下载他人分享的成熟模板使用。

- _site: 这个文件夹由jekyll生成，包含了所有静态网站需要的东东。在github上面，当你把其他的文件上传之后，系统会为你生成_site文件夹，所以，你不需要将这个文件夹上传，在.gitinore中写入：_site即可。如果需要在其他的服务器部署网站，要做的刚好相反，只要把_site中的内容（不包含这个文件夹本身）上传至根目录下即可，其他的文件夹不需要上传，因为，对于不支持jekyll的服务器而言，就算你传上去也没用。

- 其他文件夹： 你可以创建任何文件夹。如果文件夹名以下划线开头（如：_project），文件内容不会显示。如果创建了一个project文件夹，并在其中建立了一个example.md文件，那么，可以通过 sitename.com/project/example访问。对于博客写作而言，因为需要保存草稿，可以在本地建立一个_draft文件夹，将稿子暂存其中，并且不上传至服务器端，等到修改完成后，拖到post文件夹中，上传即可。

## 如何配置jekyll

上文说过，主要通过_config.yml文件来配置，主要关心两个内容：  


permalink：即文章链接的形式，包含如下几个变量：  
- year：文件名中的年份
- month 文件名中的月份
- day   文件名中的日期
- title 文件名中的标题
- categories 文章分类
- i-month 文件名中月份，除去前缀0 （如month = 04， i-month = 4）
- i-day   文件名中的日期，除去前缀0


示例的配置：  
- permalink: pretty   效果： /2011/01/23/slap-top/index.html
- permalink: /:month-:day-:year/:title.html  效果：/01-23-2011/slap-top.html


自定义内容：  
config文件中可以定义全局变量，如 title: myBlog。在文章中使用，需要用{{site.title}}来引用。jekyll会将其替代为“myBlog”


##如何使用YAML Front Matter


使用YAML定义格式的文章（关于YAML，可参考：[用jekyll构建静态网站](http://yanping.me/cn/blog/2011/12/15/building-static-sites-with-jekyll/)），需要在文章开头，使用如下的格式： 


---
 layout: post
 title: Blogging Like a Hacker
 ---


可以使用的变量：  


- layout： 调用_layouts文件夹下的一个模板，如上面例子中用了post模板
- permalink：除了在_config.yml中设置了permalink之外，还可以对单独一篇文章使用特殊的永久链接
- published：可以单独设置一篇文章是否需要发布
- category: 设置文章的分类
- tags: 设置文章标签

基本的设置就完成了。但是要在本地预览博客，还需要安装jekyll的本地环境。


## 搭建本地环境



- 下载RailInstaller并安装。
- 修改gem源：
- gem sources -remove http://rubygems.org/
- gem sources -a http://ruby.taobao.org/
- 用gem安装jekyll：
- gem install jekyll
- 与jekyll配套的一些包也会自动安装。
- 如果要用rdiscount或kramdown来解析markdown语言，也需要用如下的命令安装
- gem install rdiscount kramdown
  在_config.yml中设置：mardown: rdiscount 就可以使用rdiscount进行解析。
 
    当当当当。。。。本地环境搭建完成。cd 到博客的根目录中，然后使用命令：
    $ jekyll --server
    
 就可以通过localhost:4000来访问了。
    
## 关于中文字符的问题
    

我完成上面的步骤之后，还遇到一个问题：
打开localhost:4000之后，中文文章出现乱码，但是其它一切正常。应该是模板中符号集设置不当造成的。我直接用了一个英文博客的模板，而没有做修改。那么，如何设置，使其正常工作呢？

是在设置文件_config.yml中改动，还是要在模板文件default.html和post.html中改动？

（问题已经解决。）


     






    



    








