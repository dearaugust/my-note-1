#GITBOOK#

###使用 Gitbook 来做笔记###

先装包：
```npm
npm install gitbook-cli -g
```
创建笔记文件夹my-note并进入
```
mkdir my-note && cd my-note
```
初始化gitbook
```
gitbook init
```
这样，会生成2个文件

	 - README.md 封面
	 - SUMMARY.md 目录

启动项目：
```
gitbook serve
```
这样，可以启动一个服务器，然后到 localhost:4000 端口，就可以看到这本书了。
```
在浏览器打开：localhost:4000
```
###托管gitbook###

在github上创建my-node仓库

调整结构：新建content文件夹将README.md,SUMMARY.md文件放在里面

然后，把项目变成一个 nodejs 的项目：
```
npm init -y
```

然后，在package.json 中添加这些代码：

```
"scripts": {
 "start": "gitbook serve ./content ./gh-pages",
 "build": "gitbook build ./content ./gh-pages",
 "deploy": "node ./scripts/deploy-gh-pages.js",
 "publish": "npm run build && npm run deploy",
 "port": "lsof -i :35729"
},
```
运行
```
npm start
```
创建一个.gitignore文件将不上传的文件添加

```
# dependencies
/node_modules

/scripts
/gh-pages
```
github备份（上传）操作
```
git init
git add -A
git commit -a -m 'new'
git remote add origin https://github.com/l552177239/my-note.git
git push -u origin master
``
部署书籍到 gh-pages

 - 第一步：运行：npm run build，把md文件转化为html放到gh-pages文件夹
 - 第二步：拷贝gh-pages中的所有文件，到gh-pages分支，然后上传
 - 第三步：以后每次修改完都拷贝到gh-pages分支，很麻烦

安包：npm i gh-pages --save

在script文件夹下创建deploy-gh-pages.js
将下面代码拷贝进去
```
'use strict';

var ghpages = require('gh-pages');

main();

function main() {
    ghpages.publish('./gh-pages', console.error.bind(console));
}
```