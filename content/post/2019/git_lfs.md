---
date: 2019-12-22
title: Git LFS
categories: [技术文档]
description: >
    Git LFS（large filesystem）是Github开发的一个Git扩展，用于实现Git对大文件的支持。GitLab也支持LFS扩展。git对文本类文件能提供很好的维护支持，但是一些二进制文件，如office文件、图片等，无法被git的diff、delta很好的追踪。LFS 用于针对管理此类非文本类文件。
---

### 本地安装LFS扩展

```bash
yum install git-lfs
```
> 注意：安装Git LFS的Git版本不低于1.8.2，高版本的git自带lfs不用额外安装  

**针对某个项目进行git lfs install**

```bash
# 在某个Git仓库下
$ git lfs install
Updated pre-push hook.
Git LFS initialized.
```

这个命令会安装pre-push的git hook，即在push之前会调用一些hook执行推送large file的操作。  

### 指定LFS文件 

```bash
# track后缀为doc、docx的文件
git lfs track "*.doc"  
git lfs track "*.docx"
```
执行后仓库中会生成一个.gitattribute文件，git的勾子就是根据这个文件来判断当前仓库是否有使用LFS管理。

完成后和往常一样提交文件即可：

```bash
# 将large File添加到项目中
git add .

# 将文件的metadata写入
git commit -m "Add gemfield docx file"

# 将git repo和large file同步到gitlab server上
git push origin master
```

### remote最新的LFS

```bash
git lfs fetch origin master
```

### 文件加锁  
因为git lfs管理的是二进制文件，并不擅长解决merge之类的问题，因此它有一个特殊的概念：文件加锁（gitlab 10.5后支持）。操作流程如下：
- 先配置哪些文件是可以加锁的，语法和.gitignore类似
- 如果要准备修改一个文件了，先对这个文件加锁
- 修改完后push，然后解锁该文件  

### 历史文件问题  
新增LFS配置无法影响历史的提交记录，对于已经很庞大的仓库而言，直接这么做起不到瘦身的效果，可行的做法是重建一个仓库，把各个分支最新的快照同步过来。  
新版本使用git lfs migrate命令。  

### 常用命令
```bash
git lfs help # 查看git lfs的帮助
git lfs version # 查看git lfs的版本号
git lfs track # 查看git lfs的文件追踪信息
git lfs track '*.dll' # dll文件用lfs来管理，会在根目录的.gitattributes文件中添加：*.dll filter=lfs diff=lfs merge=lfs -text
git lfs track "*.a" "*.dylib" "*.so" "*.lib" "*.dll"  # a、dylib、so、lib、dll文件用lfs来管理，会在根目录的.gitattributes文件中添加
git lfs track 'Guid.upk' # Guid.upk文件用lfs来管理，会在根目录的.gitattributes文件中添加：Guid.upk filter=lfs diff=lfs merge=lfs -text
git lfs track 'maps/*' # 根目录下maps文件夹中的所有文件用lfs来管理，会在根目录的.gitattributes文件中添加：maps/* filter=lfs diff=lfs merge=lfs -text
git lfs untrack 'Guid.upk' # Guid.upk文件不再使用lfs来管理
git lfs status  # 查看当前git lfs对象的状态
git lfs ls-files  # 查看当前哪些文件是使用lfs管理的
git lfs clone https://github.com/kekec/Test.git # 克隆包含Git LFS的远程仓库到本地
git lfs env  # 查看环境信息
```