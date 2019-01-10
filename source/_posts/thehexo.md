---
title: thehexo
tags:
  - 搭建
date: 2019-01-09 23:35:00
---

hexo+github搭建博客
1.安装hexo
```
Node.js
git 
npm install -g hexo-cli  #安装hexo
```
2.初始化hexo
```
mkdir blog
hexo init blog # 使用 hexo 初始化 blog
hexo s # 启动服务器
```
访问http://localhost:4000/，即可看到本地的博客页面
注：初始化很慢，可先执行npm --registry https://registry.npm.taobao.org info underscore 
3.设置next主题
```
cd ~/blog
git clone https://github.com/theme-next/hexo-theme-next themes/next #将next主题的文件夹下载至themes文件夹下
vim ~/blog/_config.yml  #编辑theme: next
hexo s #重新启动服务器
```
再访问http://localhost:4000/，可见主题改变了
4.上传到 github 通过 username.github.io 访问
```
npm install hexo-deployer-git –save –registry=http://registry.npm.taobao.org #安装 hexo-deployer-git
vim ~/blog/_config.yml #配置 deploy
```
```
编辑内容为：
deploy:
type: git
repo: https://github.com/username/username.github.io.git # 替换为你的仓库路径
branch: master
```
github创建仓库 username.github.io
```
hexo d -g  #部署代码到github
```
访问https://username.github.io/
5.写文章
配置~/blog/_config.yml:
default_layout: draft
```
hexo new test #在source_drafts下新建test.md，并编辑内容
hexo publish test #将草稿publish到source_posts
hexo d -g #部署代码
```
6.设置标签
```
hexo new page about #新建about标签
hexo new page categories
hexo new page tags
vim ~/categories/index.md #编辑加上type: "categories",同about，tages
vim ~/source/_drafts/test.md #编辑文章的标签属性，加上categoties: -学习
```
本地查看关于，标签，分类三个标签已存在，且文章已归类标签

7.设置背景动态
```
next版本为5.1.1以上：
修改主题配置文件_config.yml中找到canvas_nest: false，改为canvas_nest: true即可
```
```
next版本为6.0+：
进入theme/next目录 
执行命令： git clone https://github.com/theme-next/theme-next-canvas-nest source/lib/canvas-nest
修改主题配置文件_config.yml中的canvas_nest: false改为canvas_nest: true
```
```
参数：
  onmobile: true # display on mobile or not
  color: '0,0,255' # RGB values, use ',' to separate
  opacity: 0.5 # the opacity of line: 0~1
  zIndex: -1 # z-index property of the background
  count: 99 # the number of lines
```

8.设置评论：gitment
```
在blog根目录安装gitment：
npm i --save gitment
```
```
申请应用：注册New OAuth App
Application name:随意
Homepage URL:随意
Application description:描述,随意
Authorization callback URL:这个必须写你的博客地址
申请好之后点注册,然后就可以看到ClientID和Client Secret,后面会用到
```
```
主题配置文件
# Gitment
# Introduction: https://imsun.net/posts/gitment-introduction/
gitment:
  enable: true
  mint: true # RECOMMEND, A mint on Gitment, to support count, language and proxy_gateway
  count: true # Show comments count in post meta area
  lazy: false # Comments lazy loading with a button
  cleanly: false # Hide 'Powered by ...' on footer, and more
  language: # Force language, or auto switch by theme
  github_user: #github的uesrname
  github_repo: #你的公开的git仓库,到时候评论会作为那个项目的issue
  client_id: {刚才申请的ClientID}
  client_secret: {刚才申请的Client Secret}
  proxy_gateway: # Address of api proxy, See: https://github.com/aimingoo/intersect
  redirect_protocol: # Protocol of redirect_uri with force_redirect_protocol when mint enabled
```