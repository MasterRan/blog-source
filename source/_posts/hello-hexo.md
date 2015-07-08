title: 首发
date: 2015-7-8 11:00:00
categories: hexo
tags: [hexo,随笔]
description: hexo写个博客么么嗒
---
一开始想起写博客，其实我的内心是拒绝的。可是当我翻开nodejs想着写点东西的时候，忽然发现搭个博客是个很好的练手方法，于是乎捣鼓了很久妄想写出个框架，然而残酷的现实森森的伤害了我。经过内心的煎熬与繁杂的调查后，最终选择找一个现成的框架学习一下，至于为什么选择了hexo，我能表示下是因为yilia这个主题**真的很好看吗**。。不知道我这么丧心病狂的打广告会不会被原作者约，想想还有些小激动呢⁄(⁄ ⁄•⁄ω⁄•⁄ ⁄)⁄

<!-- more -->

#环境构建篇

##安装nodejs
windows下直接下载安装一步到位，注意看好系统位数。（PS：天朝下载真真慢）

##安装git
最开始直接装的github for windows，感觉并不好用，界面本身不友好而且反应慢。。于是乎换了[msygit](http://msysgit.github.io/),下载安装一路next到头后添加环境变量
*D:\Git\bin;
D:\Git\libexec\git-core*
*D:\Git*是github的安装目录

##安装hexo
[hexo](https://hexo.io/)真的是个很好用的博客框架，基于nodejs使得它generate速度极快，并且含有丰富的模板，实在是缺乏美感的程序员必备良品。安装方法直接使用npm就可以
```
	npm install hexo-cli -g

```

>插一句如果npm下载不下来，那肯定是你(tian)自(chao)己(xia)网(zai)络(yi)有(jing)问(bei)题(qiang)。可以使用国内的npm镜像来解决。我用的是[淘宝npm镜像](http://npm.taobao.org/),具体使用方法是替换掉npm config里的registry：
>```
	npm config set registry https://registry.npm.taobao.org 
	npm info underscore
```
>如果配置成功后会有response。此时再次install发现飞一般的感觉了吧。需要注意的是如果要使用npm publish功能，则需要再改回原来的地址，具体操作为：
>	npm config set registry https://registry.npmjs.org

#建立博客

hexo命令行简洁明了，执行以下命令即可初始化
```
	hexo init <folder>
```
>也可以cd到目标目录，直接hexo init

然后进入到目录中执行npm install来安装依赖的node module。
此时一个博客已经建好了，在目录中使用hexo server，然后在浏览器中访问本机4000端口即可看到。

#上传github
这一步我做了很久，原因是原来图形界面用习惯了，这里一用bash就出现很多问题，看来平时不能偷懒啊。这里需要：
1. 注册github账号，已有的默认忽略
>这里我原来注册的账号直接用qq号做用户名，后来发现竟然不能改，正好密码又忘了，索性又申请了一个=。=
2. 建立一个仓库，名字无所谓，建议*your_name.github.com*，方便辨认
3. 添加SSH公钥到你的账户
4. 生成blog静态页面
5. 部署到github上

##github密钥设置
前两步很简单，第三步没用过的需要费点事，首先打开git bash，设置用户名密码：
```
	git config --global user.email "xxx@qq.com"
	git config --global user.name "xxx"
```
然后生成密钥：
```
	ssh-keygen -t rsa -C "xxx@qq.com"
```
>这一步会要求输入文件路径，建议用默认的就好，即直接敲回车。

至此windows用户可以在*C:/Users/your_name/.ssh*下找到两个文件*id_rsa*和*id_rsa.pub*。
接下来只需要进入github页面的Settings->SSH keys点击添加，并把*id_rsa.pub*里的内容复制过去，随便起个名字就好了。
最后可以验证一下
```
	ssh -T git@github.com
```

##部署
```
	hexo generate
```
此时项目目录中多了一个public文件夹，里面就是生成的静态文件，然后用文本编辑器（这里用的sublime2）打开*_config.yml*，大致如下：
```
	# Hexo Configuration
	## Docs: http://zespia.tw/hexo/docs/configure.html
	## Source: https://github.com/tommy351/hexo/

	# Site #整站的基本信息
	title: Jie's Blog #网站标题
	subtitle: 小清新伪文艺程序猿，求包养 #网站副标题
	description: 前端 | js |图形图像 #网站描述，给搜索引擎用的，在生成html中的head->meta中可看到
	author: Jie #网站作者，在下方显示
	email: 540269584@qq.com #联系邮箱
	language: zh-CN #语言

	# URL #域名和文件结构
	## If your site is put in a subdirectory, set url as 'http://yoursite.com/child' and root as '/child/'
	url: http://yoursite.com #你的域名
	root: /
	permalink: :year/:month/:day/:title/
	tag_dir: tags
	archive_dir: archives
	category_dir: categories
	code_dir: downloads/code

	# Writing #写文章选项
	new_post_name: :title.md # File name of new posts
	default_layout: post #默认layout方式
	auto_spacing: false # Add spaces between asian characters and western characters
	titlecase: false # Transform title into titlecase
	external_link: true # Open external links in new tab
	max_open_file: 100
	multi_thread: true
	filename_case: 0
	render_drafts: false
	highlight: #代码高亮
	  enable: true #是否启用
	  line_number: false #是否显示行号
	  tab_replace:

	# Category & Tag #分类与标签
	default_category: uncategorized # default
	category_map:
	tag_map:

	# Archives #存档，这里的说明好像不对。全部选择1，这个选项与主题中的选项有时候会有冲突
	## 2: Enable pagination
	## 1: Disable pagination
	## 0: Fully Disable
	archive: 1
	category: 1
	tag: 1

	# Server #本地服务参数
	## Hexo uses Connect as a server
	## You can customize the logger format as defined in
	## http://www.senchalabs.org/connect/logger.html
	port: 4000
	logger: true
	logger_format:

	# Date / Time format #日期显示格式
	## Hexo uses Moment.js to parse and display date
	## You can customize the date format as defined in
	## http://momentjs.com/docs/#/displaying/format/
	date_format: MMM D YYYY
	time_format: H:mm:ss

	# Pagination #分页设置
	## Set per_page to 0 to disable pagination
	per_page: 10 #每页10篇文章
	pagination_dir: page

	# Disqus #社会化评论disqus，我使用多说，在主题中配置
	disqus_shortname:

	# Extensions #插件，暂时未安装插件
	## Plugins: https://github.com/tommy351/hexo/wiki/Plugins
	## Themes: https://github.com/tommy351/hexo/wiki/Themes
	## 主题
	theme: yilia # raytaylorism # pacman # modernist # light #yilia
	exclude_generator:

	# Deployment #部署
	## Docs: http://zespia.tw/hexo/docs/deploy.html
	deploy:
	  type: github
	  repository: git@github.com:MasterRan/masterran.github.com.git #你的GitHub Pages仓库
```
部署前需要修改的地方在最下面的deploy中，把repository改成你的仓库地址就好了。
最后一步，运行命令：

```
	hexo deploy
```
>1. 提示找不到git
>	解决办法： 
>	在Hexo 3.0版本后deploy git 被分开的，所以需要安装，安装命令如下:
>		npm install hexo-deployer-git --save
>2. 部署的时候执行：hexo deploy 命令行没有任何输出，也没有错误。 
>	解决办法： 
>	在部署的_config.yml文件中，找到deploy:标签，**在每个冒号后面必须要空格**，否则就会出现上述问题。

如果没有问题的话,此时你的blog已经被上传到git上了，赶紧进入github对应仓库页面中的settings，点击链接看下吧~

#其他

##关于主题
hexo里的主题大多托管在github上，可以参见[主题列表](https://github.com/hexojs/hexo/wiki/Themes)，本博使用的主题是[yilia](https://github.com/litten/hexo-theme-yilia)，进行了一些小的样式修改而已。所有的主题都可以通过git命令来下载：

	git clone git@github.com:litten/hexo-theme-yilia.git

下载完毕后放到theme下就可以了。

##关于hexo
关于hexo的各种操作
```
	hexo new "postName" #新建文章
	hexo new page "pageName" #新建页面
	hexo generate #生成静态页面至public目录
	hexo server #开启预览访问端口（默认端口4000，'ctrl + c'关闭server）
	hexo deploy #将.deploy目录部署到GitHub
```