---
date: 2020-04-22
title: 静态网站框架
categories: [技术文档]
tags: ["web"]
sidebar: false
description: 静态网站生成框架流行界的宠儿们……
---

## Hugo
### 目录结构
```bash
 ▸ archetypes/    # 包括内容类型，在创建新内容时自动生成内容的配置
 ▸ content/       # 包括网站内容，全部使用markdown格式
 ▸ data/
 ▸ layouts/       # 包括了网站的模版，决定内容如何呈现
 ▸ static/        # 包括了css, js, fonts, media等，决定网站的外观
 ▸ themes/
   config.toml

 ▸ resources  # Caches some files to speed up generation.
```

**文章**：以markdown格式的文件存放在content目录下面
```bash
└── content
    ├── _index.md          // [home]            <- https://example.com/ **
    ├── about.md           // [page]            <- https://example.com/about/
    ├── posts               
    |   ├── _index.md      // [section]         <- https://example.com/posts/ **         
    |   ├── firstpost.md   // [page]            <- https://example.com/posts/firstpost/
    |   ├── happy           
    |   |   ├── _index.md  // [section]         <- https://example.com/posts/happy/ **
    |   |   └── ness.md    // [page]            <- https://example.com/posts/happy/ness/
    |   └── secondpost.md  // [page]            <- https://example.com/posts/secondpost/
    └── quote   
        ├── _index.md      // [section]         <- https://example.com/quote/ **           
        ├── first.md       // [page]            <- https://example.com/quote/first/
        └── second.md      // [page]            <- https://example.com/quote/second/

// hugo默认生成的页面, 没有对应的markdown文章
分类列表页面               // [taxonomyTerm]    <- https://example.com/categories/  **
某个分类下的所有文章的列表  // [taxonomy]        <- https://example.com/categories/one-category  **
标签列表页面               // [taxonomyTerm]    <- https://example.com/tags/  **
某个标签下的所有文章的列表  // [taxonomy]        <- https://example.com/tags/one-tag  **
```
**模版**：模板（皮肤）页面存放在两个地方 
三种类型的模版：single、list and partial。Hugo有一套自己的模版查找机制，如果找不到与内容完全匹配的模板，它将向上移动一级并从那里搜索。直到找到匹配的模板或用完模板来尝试。如果找不到模板，它将使用该站点的默认模板。      
```bash
├── layouts   // 默认为空
└── themes
    └── mytheme
        └── layouts
            ├── 404.html             // 404页面模板
            ├── _default
            │   ├── baseof.html      // 默认的基础模板页, 使用的方式是'拼接', 而不是'继承'.
            │   ├── list.html        // 列表模板  
            │   └── single.html      // 单页模板
            ├── index.html           // 首页模板
            └── partials             // 局部模板, 通过partial引入
                ├── footer.html
                ├── header.html
                └── head.html       
```
皮肤列表： https://www.gohugo.org/theme/  

**页面**：页面就是通过hugo 最终生成的静态网站中的html页面. 页面是由两部内容合成的, 即: 页面 = 文章 + 模板. hugo会根据一定的规制去寻找文章对应的模板页面, 从而生成页面.
0.60前的版本采用 BlackFriday 作为markdown解析器，0.60后版本默认采用Goldmark作为markdown解析器。   

### 安装
```bash
tar -zxvf ./hugo_0.69.2_Linux-64bit.tar.gz
mv ./hugo /usr/local/bin/
hugo version
```  
如果是hugo extended版本，CentOS7会遇到libstdc++.so.6.0版本过低问题，需要使用新的gcc动态库  
```bash
# 下载新的动态库libstdc++.so.6.0.26上传到/usr/lib64
chmod 755 libstdc++.so.6.0.26 # 增加执行权限
rm -rf libstdc++.so.6 # 删除原来软连接
ln -s libstdc++.so.6.0.26 libstdc++.so.6 # 将默认库的软连接指向最新动态库
strings /usr/lib64/libstdc++.so.6 | grep GLIBC # 默认动态库升级完成。重新运行以下命令检查动态库
```

### 部署
假设你需要部署在 GitHub Pages 上，首先在GitHub上创建一个Repository，命名为：coderzh.github.io （coderzh替换为你的github用户名）。
```bash
hugo --theme=hyde --baseUrl="http://coderzh.github.io/"
```
（注意，以上命令并不会生成草稿页面，如果未生成任何文章，请去掉文章头部的 draft=true 再重新生成。）

如果一切顺利，所有静态页面都会生成到 public 目录，将pubilc目录里所有文件 push 到刚创建的Repository的 master 分支。  
```bash
cd public
git init
git remote add origin https://github.com/coderzh/coderzh.github.io.git
git add -A
git commit -m "first commit"
git push -u origin master
```
浏览器里访问：http://coderzh.github.io/

**Hugo server**
`hugo server -D` Navigate to your new site at http://localhost:1313/.

`hugo server -t hyde --buildDrafts --baseURL=http://106.54.3.157 --bind= --port=80`-t参数的意思是使用hyde主题渲染我们的页面，作为草稿，即draft参数设置为true，运行Hugo时要加上--buildDrafts参数才会生成被标记为草稿的页面，后面参数如不加默认在浏览器localhost:1313访问。发布在当前目录public/，如果使用Github pages来作为博客的Host，你只需要将public/里的文件上传即可。

### Hugo pipe

### 使用httpd发布
```bash
yum install httpd
```

配置文件`/etc/httpd/conf/httpd.conf`   
默认web站点目录的路径: DocumentRoot "/var/www/html"  
默认http端口：80  

```bash
# hugo 生成的public目录
cp -R ./public/* /var/www/html/
service httpd start # 启动
service httpd restart # 重新启动 
service httpd stop # 停止服务
```

### 页面绑定
hugo中的内容组织是依赖Page Bundles来管理的。Page Bundles包括Leaf Bundle（没有子节点）和Branch Bundle（home page, section, taxonomy terms, taxonomy list）两类。  
| |**Leaf Bundle**|**Branch Bundle**|
|---|---|---|
|索引文件|index.md|_index.md|
|布局类型|single|list|
|嵌套|不允许嵌套|允许Leaf或Branch Bundle嵌套|

**Section**是基于content/目录下的组织结构定义的页面集合。  
content/ 下的第一级子目录都是一个section。如果想让一个子目录成为section，需要在目录下面定义_index.md文件。 所有的section构成一个section tree。  
```
content
└── blog        <-- Section, 因为是content的子目录
    ├── funny-cats
    │   ├── mypost.md
    │   └── kittens         <-- Section, 因为包含_index.md
    │       └── _index.md
    └── tech                <-- Section, 因为包含 _index.md
        └── _index.md
```
如果section tree 需要可导航，至少最底层的部分需要定义一个_index.md文件。  

front matter 用来配置文章的标题、时间、链接、分类等元信息，提供给模板调用，支持toml和yaml配置  
```toml
+++
title = "post title"
description = "description."
date = "2018-08-20"
tags = [ "tag1", "tag2", "tag3"]
categories = ["cat1","cat2"]
weight = 20
+++
```
```
                               url ("/posts/my-first-hugo-post/")
                   ⊢------------^----------⊣
       baseurl     section     slug
⊢--------^--------⊣⊢-^--⊣⊢-------^---------⊣
                 permalink
⊢--------------------^---------------------⊣
https://example.com/posts/my-first-hugo-post/index.html
```

### Configuration
```
├── config
│   ├── _default
│   │   ├── config.toml
│   │   ├── languages.toml
│   │   ├── menus.en.toml
│   │   ├── menus.zh.toml
│   │   └── params.toml
│   ├── production
│   │   ├── config.toml
│   │   └── params.toml
│   └── staging
│       ├── config.toml
│       └── params.toml
```

## Gatsby


## Vuepress
VuePress 遵循 “约定优于配置” 的原则，推荐的目录结构如下：  
```
├── docs
│   ├── .vuepress (可选的)
│   │   ├── components (可选的)
│   │   ├── theme (可选的)
│   │   │   └── Layout.vue
│   │   ├── public (可选的)
│   │   ├── styles (可选的)
│   │   │   ├── index.styl
│   │   │   └── palette.styl
│   │   ├── templates (可选的, 谨慎配置)
│   │   │   ├── dev.html
│   │   │   └── ssr.html
│   │   ├── config.js (可选的)
│   │   └── enhanceApp.js (可选的)
│   │ 
│   ├── README.md
│   ├── guide
│   │   └── README.md
│   └── config.md
│ 
└── package.json
```

- docs/.vuepress: 用于存放全局的配置、组件、静态资源等。
- docs/.vuepress/components: 该目录中的 Vue 组件将会被自动注册为全局组件。
- docs/.vuepress/theme: 用于存放本地主题。
- docs/.vuepress/styles: 用于存放样式相关的文件。
- docs/.vuepress/styles/index.styl: 将会被自动应用的全局样式文件，会生成在最终的 CSS 文件结尾，具有比默认样式更高的优先级。
- docs/.vuepress/styles/palette.styl: 用于重写默认颜色常量，或者设置新的 stylus 颜色常量。
- docs/.vuepress/public: 静态资源目录。
- docs/.vuepress/templates: 存储 HTML 模板文件。
- docs/.vuepress/templates/dev.html: 用于开发环境的 HTML 模板文件。
- docs/.vuepress/templates/ssr.html: 构建时基于 Vue SSR 的 HTML 模板文件。
- docs/.vuepress/config.js: 配置文件的入口文件，也可以是 YML 或 toml。
- docs/.vuepress/enhanceApp.js: 客户端应用的增强。

注意图片静态资源尽量不要用中文，否则编译时需要用markdown-it转换处理

---

### [Vuepress-docker](https://hub.docker.com/r/blasteh/vuepress)
Simple build of vuepress using Alpine Linux on Docker.

The image has 2 folders, 1 for input files, 1 for output files.
Mount these folders to use the image:

Input folder: `/root/src`

Output folder: `/root/html`

When the build runs, it will take contents of the input folder, generate the site, and then place them in the output folder.
This image regenerates the files every 23 hours unless you use the hook option.
Webhook is supplied by [Hookdoo](https://github.com/adnanh/webhook)

#### Environment variables
`USE_HOOK` - The web hook is enabled as long as this is present.

`GITHUB_REPO` - Remove "https://" from the url; e.g. use `GITHUB_REPO=github.com/blastehh/vuepress-docker.git` instead of `GITHUB_REPO=https://github.com/blastehh/vuepress-docker.git`

`GITHUB_TOKEN` - Needed to access private repos, otherwise will try to access a public repo.

`GITHUB_PUSH_REPO` - URL of repo to push to once build finishes, e.g. `github.com/blastehh/mypage.git`

`GITHUB_PUSH_TOKEN` - Set the token for pushing to Github if different from `GITHUB_TOKEN`

#### Example docker command
This will automatically regenerate the source files every 23 hours.
```bash
docker run --name vuepress -v /host/vuepress/files/:/root/src/:rw -v /host/vuepress/output/:/root/html/:rw -d blasteh/vuepress
```

#### Github example:
This will pull from the repo before generating the files.
```bash
docker run --name vuepress -v /host/vuepress/files/:/root/src/:rw -v /host/vuepress/output/:/root/html/:rw -d -e GITHUB_REPO=github.com/blastehh/vuepress-docker.git blasteh/vuepress
```

#### Github example with a [Personal access token](https://github.com/settings/tokens):
This will pull from a private repo before generating the files.
```
docker run --name vuepress -v /host/vuepress/files/:/root/src/:rw -v /host/vuepress/output/:/root/html/:rw -d -e GITHUB_REPO=github.com/blastehh/vuepress-docker.git -e GITHUB_TOKEN=TOKENHERE blasteh/vuepress
```

#### Github with hooks example:
This will listen for a webhook, and then pull from a private repo before generating the files.
Trigger the hook via `http://<container address>:9000/hooks/vuepress-webhook`
```
docker run --name vuepress -v /host/vuepress/files/:/root/src/:rw -v /host/vuepress/output/:/root/html/:rw -d -p 9000:9000 -e USE_HOOK=1 -e GITHUB_REPO=github.com/blastehh/vuepress-docker.git -e GITHUB_TOKEN=TOKENHERE blasteh/vuepress
```
## Hexo

## Gitbook 
前提已安装Node，执行  
```bash
npm install gitbook-cli -g
```
gitbook-cli 是 gitbook 的一个命令行工具, 通过它安装和管理 gitbook 的多个版本.

```bash
mkdir mybook
gitbook init
gitbook serve # 启动gitbook项目并提供http://localhost:4000为浏览器浏览链接。
gitbook help # 列出gitbook所有的命令
gitbook --help # 输出gitbook-cli的帮助信息
gitbook build # 生成静态网页
gitbook serve # 生成静态网页并运行服务器
gitbook build --gitbook=2.0.1 # 生成时指定gitbook的版本, 本地没有会先下载
gitbook ls # 列出本地所有的gitbook版本
gitbook ls-remote # 列出远程可用的gitbook版本
gitbook fetch 标签/版本号 # 安装对应的gitbook版本
gitbook update # 更新到gitbook的最新版本
gitbook uninstall 2.0.1 # 卸载对应的gitbook版本
gitbook build --log=debug # 指定log的级别
gitbook builid --debug # 输出错误信息
gitbook build[path] # 构建gitbook项目，构建路径可省略，默认为_book
```

## Docsify
#### 手动创建方法
在项目中创建一个index.html文件够如下
```html
<!DOCTYPE html>
<html>
<head>
  <meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1">
  <meta name="viewport" content="width=device-width,initial-scale=1">
  <meta charset="UTF-8">
  <link rel="stylesheet" href="//unpkg.com/docsify/themes/vue.css">
</head>
<body>
  <div id="app"></div>
  <script>
    window.$docsify = {
      //...
    }
  </script>
  <script src="//unpkg.com/docsify/lib/docsify.min.js"></script>
</body>
</html>
```
然后在项目中创建.md文件  
可在终端输入npm install http-server -g来安装http-server  
>注意：  
>1.在此模式下编辑文件保存后，需要手动刷新浏览器才能看见修改的效果，下面介绍的docsify-cli可实现自动查看效果。  
>2.强烈建议把index.html文件中的docsify.min.js和vue.css文件复制到本地项目，然后使用如下方式引入：  
>```
><link rel="stylesheet" href="./vue.css">
><script src="./docsify.min.js"></script>
>```
>这样做的好处是不在依赖网络环境了。  

#### 使用docsify-cli安装
联网情况使用 `npm i docsify-cli -g` 进行全局安装    

离线安装   
```bash
tar -zvxf docsify-cli-4.4.0.tar.gz -C /usr/local/node/lib/node_modules/docsify-cli
```
#### GitLab pages部署docsify  
如果你正在部署你的主分支, 在 .gitlab-ci.yml 中包含以下脚本：  
.public 的解决方法是这样的，cp 不会无限循环的将 public/ 复制到自身。

```yml
pages:
  stage: deploy
  script:
  - mkdir .public
  - cp -r * .public
  - mv .public public
  artifacts:
    paths:
    - public
  only:
  - master
```

你可以用 `- cp -r docs/. public` 替换脚本, 如果 ./docs 是你的 docsify 子文件夹。
