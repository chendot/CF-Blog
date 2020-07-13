---
date: 2019-09-30
title: Git 常见问题
categories: [技术文档]
description: git使用中遇到的问题
sidebar: false
---

### Win7 本地速度慢

启用并行索引预加载：
```bash
git config core.preloadindex true
```

禁用UAC和luafv驱动程序（需要重启），在regedit中将`HKEY_LOCAL_MACHINE/SYSTEM/CurrentControlSet/Services/luafv`的“start”键`HKEY_LOCAL_MACHINE/SYSTEM/CurrentControlSet/Services/luafv`为4以禁用驱动程序。 然后，将UAC置于其最低设置“永不通知”

### .gitignore无效
如果某个文件已经存在于远程仓库了，也就是说某个文件已经被版本控制了，如果将该文件添加到.gitignore中，是无法生效的。因为.gitignore是用来控制尚未被纳入版本控制的文件，如果文件已经存在于远程库中，自然也就无法生效了。  
#### 方法一

直接在远程库里将想要忽略的文件删除掉，再将该文件写入.gitignore中即可。  
这种做法的前提是，你确定该文件是允许从远程库删除掉的，然而有些时候，这种做法是不可能的。要么没权限去远程库删掉该文件，要么该文件是必须的。

#### 方法二

使用命令`git rm --cached filename`[^1]，然后将该文件写入.gitignore中即可。  
该命令表示从git仓库中将文件移除，不再进行版本控制，但保留工作区的该文件。  
需要注意的是，该命令其实和方法一差不多。`git rm`表示移除某个文件，`--cached`表示从暂存区中移除，如果不加该参数就是直接从工作区移除了。

`git rm --cached filename`并不会从物理上删除文件，只是从暂存区中将文件删除。由于该文件原本已经被版本控制了，使用了该命令后，虽然保留了工作区的该文件，但是却会在暂存区中生成一个删除了该文件的记录，如果此时进行commit，就会把版本库里的该文件给删掉了，如果push到远程库，也会被删掉。最终还是走的方法一的路子。  

[^1]:>`git rm --cached filename`的补充：
    >- 新建文件1.txt，未被跟踪(Untracked files)，提交到暂存区(Changed to be committed)，未提交到版本库。使用`git rm -cached 1.txt`把文件恢复到未被跟踪的状态，即删除暂存区中的1.txt   
    >- 文件1.txt，已经提交到版本库，工作区、暂存区都是干净的。使用`git rm —cached 1.txt`把工作区的文件1.txt置为了”未跟踪”状态，即Untracked files。暂存区生成一个deleted 1.txt的记录，如果提交了，就是把版本库中的1.txt删除。不影响工作区中的文件。
    >- 文件1.txt, 已经提交到版本库，修改1.txt，并且提交到了暂存区。使用`git rm —cached 1.txt`把工作区的文件1.txt置为了”未跟踪”状态，即Untracked files。暂存区生成一个deleted 1.txt的记录，如果提交了，就是把版本库中的1.txt删除。不影响工作区中的文件。还是修改后的1.txt   
    >- 文件1.txt, 已经提交到版本库，修改1.txt，提交到暂存区，继续修改1.txt。使用`git rm —cached 1.txt`会报错，不能执行操作。  

### 远程仓库连接权限问题
#### 403错误
**方案一**    
windows系统下清理系统存储用户密码，运行   
`rundll32.exe keymgr.dll,KRShowKeyMgr`

**方案二**    
1.在代码的.git/config文件内[remote “origin”]的url的gitlab域名前添加gitlab注册时的“用户名:密码@”   
2.这个用户要在对应项目下的角色是Owner或Master才行，如果是Guest、Reporter、Developer，则如下操作后也是不行。   

**方案三**    
改成ssh方式

#### LFS: Authorization error
在 .git/config 中增加  
```
[lfs "https://git.lug.ustc.edu.cn/chendot/libbar.git/info/lfs"]
	locksverify = true
	access = basic
```

### Pull 冲突处理
git pull 远端到本地冲突时，大部分IDE git插件会自动完成冲突比较。  
如未生成自动比较结果也可参考如下处理：    
stash（将本地代码隐藏保存）-> 重新 pull -> stash pop -> 冲突修改 

### 无法识别LFS管理文件
低版本git直接clone后可能出现无法识别LFS管理文件，可尝试如下方法解决：  
```bash
# 在本地仓库目录下调用git命令  
git lfs uninstall
git reset --hard
git lfs install
git lfs pull
```  
**如果执行git reset --hard 回退版本的时候出现问题**，可参考以下方法：  
执行之前最好先用`git log --name-only`命令查看本地的版本是否有远程库最新的版本（更新过lfs插件的版本）   
1. 如果没有需要先pull代码。   
2. 如果有但是比本地最新的版本低，则需要执行`git reset --hard`版本id(前六位即可)去回退到对应版本。（该情况一般发生在本地库不小心覆盖了远端的情况）   
3. 如果有且和远程库版本信息一致，则可正常执行。   

### checking out 无响应
**如果遇到reset的时候卡在checking out files进度比是100%不动**，可能是git的安装方式出了问题。此时可卸载git,在重装的时候勾选   
```
Use  Window's default console window   
Use the native Windows Secure Channel Library
```
再重新执行`git reset --hard`，此时会卡在和之前同一行，但是有不足100%的进度比。此时可以按enter键，会提示输入用户名密码，即可继续拉取。     
再执行后续命令。项目中的问题等待片刻即可恢复正常。     

如果卡住不动用ctrl+c结束了回退，此时进程并没有真正结束，可以在本地库.git目录中将index.lock文件删除，再进行下一次的reset。   

远程被覆盖的话，用命令行可在本地reset回退到对应版本，然后执行`git push -f -u origin`分支名 用该的版本去再次替换远程代码即可。