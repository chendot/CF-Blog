---
date: 2019-08-10
title: 代码提交
sidebar: false
thumbnail: "img/git-workflow.png"
description: Git 提交注意事项
categories: [技术文档]
tags: [Git]
---

### .gitignore 配置
设置忽略规则，来过滤特定文件的提交。 

常见场景：在使用git add .的时候，遇到把你不想提交的文件也添加到了缓存中的情况，如项目本地配置，push到远端仓库会造成其他人pull冲突；又或者将大量依赖的jar包等不需要做版本控制的文件push到远端，增加仓库存储负担。

为避免提交时误操作或手动过滤上述文件的麻烦，可通过在.gitignore文件中申明不希望添加到git中去的文件，这样当使用git add .的时候这些文件就会被自动忽略掉。  

#### 忽略文件原则
>- 忽略操作系统自动生成的文件，比如缩略图等
>- 忽略编译生成的中间文件、可执行文件等，比如Java编译产生的.class文件
>- 忽略你自己的带有敏感信息的配置文件，比如存放口令的配置文件 
>- 忽略日志文件   
  
#### 忽略规则说明 

```
# 表示此为注释,将被Git忽略
*.a 表示忽略所有 .a 结尾的文件
!lib.a 表示但lib.a除外
/TODO表示仅仅忽略项目根目录下的 TODO 文件，不包括 subdir/TODO
build/ 表示忽略 build/目录下的所有文件，过滤整个build文件夹；
doc/*.txt 表示会忽略doc/notes.txt但不包括 doc/server/arch.txt
bin/: 表示忽略当前路径下的bin文件夹，该文件夹下的所有内容都会被忽略，不忽略 bin 文件
/bin: 表示忽略根目录下的bin文件
/*.c: 表示忽略cat.c，不忽略 build/cat.c
debug/*.obj: 表示忽略debug/io.obj，不忽略 debug/common/io.obj和tools/debug/io.obj
**/foo: 表示忽略/foo,a/foo,a/b/foo等
a/**/b: 表示忽略a/b, a/x/b,a/x/y/b等
!/bin/run.sh 表示不忽略bin目录下的run.sh文件
*.log: 表示忽略所有 .log 文件
config.php: 表示忽略当前路径的 config.php 文件
/mtk/表示过滤整个文件夹
*.zip 表示过滤所有.zip文件
/mtk/do.c 表示过滤某个具体文件
被过滤掉的文件就不会出现在git仓库中（gitlab或github）了，当然本地库中还有，只是push的时候不会上传。
需要注意的是，gitignore还可以指定要将哪些文件添加到版本管理中，如下：
!*.zip
!/mtk/one.txt
唯一的区别就是规则开头多了一个感叹号，Git会将满足这类规则的文件添加到版本管理中。为什么要有两种规则呢？
想象一个场景：假如我们只需要管理/mtk/目录中的one.txt文件，这个目录中的其他文件都不需要管理，那么.gitignore规则应写为：：
/mtk/*
!/mtk/one.txt
假设我们只有过滤规则，而没有添加规则，那么我们就需要把/mtk/目录下除了one.txt以外的所有文件都写出来！
注意上面的/mtk/*不能写为/mtk/，否则父目录被前面的规则排除掉了，one.txt文件虽然加了!过滤规则，也不会生效！
```

补充规则：  
```
fd1/*
说明：忽略目录 fd1 下的全部内容；注意，不管是根目录下的 /fd1/目录，还是某个子目录 /child/fd1/目录，都会被忽略；
/fd1/*
说明：忽略根目录下的 /fd1/目录的全部内容；
/*
!.gitignore
!/fw/
/fw/*
!/fw/bin/
!/fw/sf/
说明：忽略全部内容，但是不忽略 .gitignore 文件、根目录下的 /fw/bin/和 /fw/sf/目录；注意要先对bin/的父目录使用!规则，使其不被排除。
```  
#### track文件处理
对于已track的文件需要加入igonre，需先清除本地缓存(改变成untrack状态)
```bash
git rm -r -f --cached .  # 表示清除项目中所有文件的本地缓存
git rm -r --cached xxx    # xxx表示不想版本控制的文件，比如小编可以输入test.o
                        # .gitignore中的忽略规则应该与之相对应
git add .   # 添加除了忽略文件外的所有文件
git commit -m "此处可以描述你提交的信息"
git push -f # 强制推送
```

### 非文本文件提交  
采用git LFS（参考[GitLFS](./代码托管/git-lfs.md)）进行管理  