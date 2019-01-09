---
title: thehexo
tags:
- 搭建
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
vim ~/blog/_config.yml  #编辑：theme: next
hexo s #重新启动服务器
```
再访问http://localhost:4000/，可见主题改变了
4.上传到 github 通过 username.github.io 访问
```
npm install hexo-deployer-git –save –registry=http://registry.npm.taobao.org #安装 hexo-deployer-git
vim ~/blog/_config.yml #配置 deploy
```
编辑内容为：
deploy:
type: git
repo: https://github.com/username/username.github.io.git # 替换为你的仓库路径
branch: master

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
~/blog/_config.yml中的menu对应标签放开
本地查看关于，标签，分类三个标签已存在，且文章已归类标签