---
date: 2019-11-06
title: GitLab CI/CD
sidebar: false
description: GitLab内置持续集成工具 CI/CD，由配置文件 .gitlab-ci.yml 和 GitLab Runner 协调实现项目持续集成。
categories:
  - "技术文档"
tags: ["SCM","DevOps"]
---

本地开发（developing）--》静态代码走查（linting）--》单元测试（testing）--》合并到主干（merging）--》自动构建（building）--》自动发布（publishing）

![cicd](/img/cicd.png)

## 相关概念 

- **管道（pipeline）**  
每个推送到 GitLab 的提交都会产生一个与该提交关联的管道，若一次推送包含了多个提交，则管道与最后那个提交相关联，管道就是一个分成不同阶段(stage)的作业(job)的集合。
- **阶段（stage）**   
阶段是对批量作业的一个逻辑划分，每个 GitLab CI/CD 必须包含至少一个 Stage。多个 Stage 按照顺序执行，其中任何一个 Stage 失败，后续的 Stage 均不会被执行，整个CI过程被认为失败。  
- **作业（job）**  
Job被定义为顶级元素，并且至少包括一条script语句，如果一个 Job 没有显式地关联某个 Stage，则会被默认关联到 test Stage。随着项目越来越大，Job 越来越多，Job 中包含的重复逻辑可能会让配置文件臃肿不堪。.gitlab-ci.yml 中提供了 before_script 和 after_script 两个全局配置项。这两个配置项在所有 Job 的 script 执行前和执行后调用。  
 
![image](/img/gitlab-ci-cd.jpeg)  

### GitLab Runner
用来执行.gitlab-ci.yml 脚本的工具。可以理解成，Runner就像认真工作的工人，GitLab-CI就是管理工人的中心，所有工人都要在GitLab-CI里面注册，并且表明自己是为哪个项目服务。当相应的项目发生变化时，GitLab-CI就会通知相应的工人执行对应的脚本。  
> **Runner类型**  
> - Shared Runner：所有工程共用，由系统管理员创建。  
> - Specific Runer：特定项目使用  

**安装**  
V10 以后的版本的安装包为gitlab-runner  
老版本的为gitlab-ci-multi-runner  
```bash 
rpm -ivh gitlab-runner-12.9.0-1.x86_64.rpm
```
**注册Token**  
安装好Runner后，需要向Gitlab注册，在Gitlab获取token。执行
```
gitlab-runner register      # 新版本命令
gitlab-ci-multi-runner register  # 老版本命令
```

根据提示输入url和token，描述，tag，executor。  
注册完成后在 setting->CI/CD 页面会新增一条runner记录。可以进入修改配置，包括注册时输入的tag，和是否触发untag的代码    

### .gitlab-ci.yml  
.gitlab-ci.yml中可根据需要自定义执行代码走查、构建、打包、部署、测试等工作。

.gitlab-ci.yml 参数列表

| 值                                                                     | 是否必须 | 描述                                                   |
|-----------------------------|------|---------------------|
| script                                                                | yes  | 由Runner执行的shell脚本或命令                                 |
| image                                                                 | no   | 使用的docker镜像                                          |
| services                                                              | no   | 使用的docker服务镜像                                        |
| before\_script                                                        | no   | 在作业之前执行的脚本或命令                                        |
| after\_script                                                         | no   | 在作业之后执行的脚本或命令                                        |
| stages                                                                | no   | 一个pipeline的各个阶段                                      |
| stage                                                                 | no   | 一个job阶段，默认是test                                      |
| only                                                                  | no   | 限制job什么时候执行                                          |
| except                                                                | no   | 限制job什么时候不执行                                         |
| rules                                                                 | no   | 指定条件列表去确定一个job的可选属性以及是否执行该job。不可与only/except一起使用     |
| tags                                                                  | no   | 指定job适用的runner，tags为runner标签                         |
| allow\_failure                                                        | no   | 允许job失败，如果失败将不会改变提交状态                                |
| when                                                                  | no   | 指定job什么时候执行，可以是on\_success、on\_failure、always和manual |
| environment                                                           | no   | 指定job部署的环境名称                                         |
| cache                                                                 | no   | 在后续运行之间应该缓存的文件列表                                     |
| artifacts                                                             | no   | 要附加到一个job上的文件和目录列表                                   |
| dependencies                                                          | no   | 通过提供要从中获取artifacts的job列表来限制将哪些artifacts传递给特定的job     |
| coverage                                                              | no   | 设置一个给定job的代码覆盖率                                      |
| retry                                                                 | no   | job失败后的自动重试次数                                        |
| timeout                                                               | no   | 设置优先于项目范围的job超时时间                                    |
| parallel                                                              | no   | 一个job并行运行的实例数量                                       |
| trigger                                                               | no   | 定义下游pipeline的触发器                                     |
| include                                                               | no   | 允许该job包含外部YAML文件                                     |
| extends                                                               | no   | 一个job将继承的配置项                                         |
| pages                                                                 | no   | 上传job的结果与GitLab Pages一起使用                            |
| variables                                                             | no   | 在job级别上定义变量                                          |
| interruptible                                                         | no   | 定义一个job在因为新的运行而变得多余时是否可以取消                           |

### 配置示例 

示例1：  
```yml
stages:
  - pull_code_test
  - pull_code_production
  - install_deps
  - test
  - build
  - deploy_test
  - deploy_production
  
variables:
  PHP_FPM_CONTAINER: lnmp-php-fpm
  WORK_DIR: /usr/share/nginx/html/
  PROJECT: laravel-demo
  GIT_DIR: /mnt/lnmp-docker
  
# 拉取代码
pull_code_test:
  stage: pull_code_test
  only:
    - develop
  script:
     - cd ${GIT_DIR}/${PROJECT}
     - git pull origin develop
     
pull_code_production:
  stage: pull_code_production
  only:
    - master
  script:
    - cd ${GIT_DIR}/${PROJECT}
    - git pull origin master
    
# 安装依赖
install_deps:
  stage: install_deps
  script:
    - docker exec -w ${WORK_DIR}/${PROJECT} ${PHP_FPM_CONTAINER} composer install
    
build:
  stage: build
  script:
    # Run migrations
    - docker exec -w ${WORK_DIR}/${PROJECT} ${PHP_FPM_CONTAINER} php artisan migrate
    # Cache clearing
    - docker exec -w ${WORK_DIR}/${PROJECT} ${PHP_FPM_CONTAINER} php artisan cache:clear
    # Create a cache file for faster configuration loading
    - docker exec -w ${WORK_DIR}/${PROJECT} ${PHP_FPM_CONTAINER} php artisan config:cache
    # Create a route cache file for faster route registration
    - docker exec -w ${WORK_DIR}/${PROJECT} ${PHP_FPM_CONTAINER} php artisan route:clear
    
deploy_test:
  stage: deploy_test
  script:
    - cd ${GIT_DIR}
    - docker-compose down && docker-compose build && docker-compose up -d
    
deploy_production:
  stage: deploy_production
  script:
    - cd ${GIT_DIR}
    - docker-compose restart
```
示例2：  
```yml
# general settings for all
.general: &general
  stage: deploy     #定义构建场景为部署，1.init初始化、2.lint代码规范、3.unit_test单元测试、4.build构建、5.deploy部署，若其中任务一个步骤出错，都不会到部署
  only:
    - hotfix/hotfix-conference      #指定分支名为紧急修bug，master主开发分支、feature新功能分支、release发布分支、hotfix紧急修bug分支
  when: manual   #触发条件为手工执行
  tags:
    - cloud         #指定在哪个ci runner工作，云
  image: ip:30050/builder/maven:v1-alpine      #青云maven容器
  script:
    - echo "current branch ****** $CI_COMMIT_REF_NAME ******"
    - echo "deploy start ..."
 
    - /share/script/deploy.sh $CI_JOB_NAME     #执行脚本，此脚本路径是被映射至gitlab runner容器内的路径，参数为CI_JOB_NAME变量
     
    - echo "deploy done."
 
# general settings for dev
.dev: &dev        #开发环境
  <<: *general    #继承general定义的变量，若重新定义将被覆盖
  tags:
    - local     #本地
  image: ip:30050/builder/maven:v1-alpine   #本地maven容器
 
 
# golive deploy setting
.golive: &golive  
  <<: *general  #继承general定义的变量，若再定义将被覆盖
  only:
    - master    #指定分支名
  script:
    - echo "current branch ****** $CI_COMMIT_REF_NAME ******"
    - echo "deploy golive start ..."
 
    - /share/script/golive/deploy.sh $CI_JOB_NAME
     
    - echo "deploy golive done."
 
 
#######定义hotfix/hotfix-conference 分支使用dev使用dev job的配置、test使用 general job的配置  
# deploy discovery
discovery - dev: *dev
discovery - test: *general
 
# deploy services
services - dev: *dev
services - test: *general
 
######定义仅master分支使用golive job定义的配置
backend - staging - node1: *golive
backend - staging - node2: *golive
 
backend - prod - node1: *golive  
backend - prod - node2: *golive
```
## 常用参数
### environment
用于定义job部署到特殊的环境中。如果指定了environment，并且没有该名下的环境则会自动创建  
```yml
enviroment:
  name: uat
  url: https://test.com # 如果job成功会在environment/deployment页面中创建一个合并请求按钮指向该地址
```
### artifacts
用于指定成功后生成物（构建物）。只能使用项目工作目录下的文件或目录路径。job成功后会将artifacts发送到GitLab，可在页面UI中下载
```yml
artifacts:  # 生成构建物，可供其它Job使用，同时可在GitLab页面对应管道流程下载
    name: "$CI_JOB_NAME"
    #untracked: true # 传递所有git没有追踪的文件
    expire_in: 1 week
    paths:  # 只能使用项目工作目录下文件或路径
      - dlqs/dlqs.war
      - changelog.txt
      - dlqs/deploy.sh
```
### image和services
image：所要使用的docker镜像  
services：所要使用的dockers服务

### only
默认是or的关系
```yml
only: # 有一个条件满足就会触发
  - master
  - merge_requests
```
### pages
管道触发会执行pages的自动部署，将我们的页面发布到GitLab Pages服务中。
```yml
pages:
  cache:
    paths:
    - node_modules/

  script:
  - cp -r docs/. .public
  
  artifacts:
    paths:
    - public
  
  only:
  - master
```

---
> edited by Shuzheng

## 应用实例

### 安装 git
yum -y install git (针对el7系统会自带git 1.8.3符合lfs插件版本)
在/etc/profile中配置环境变量（示例）：
export PATH=/usr/libexec/bin:$PATH

rpm –ivh  lfs的rpm包。

### 安装构建工具
安装jdk：  
手动上传jdk的安装包到/usr/local目录下，解压即可
在/etc/profile中配置环境变量（示例）：
```bash
export JAVA_HOME=/usr/local/jdk1.8.0_162
export CLASSPATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar
export PATH=$PATH:$JAVA_HOME/bin
```

手动上传ant的安装包到/usr目录下，解压即可。然后在/etc/profile中配置环境变量（示例）：
```bash
export ANT_HOME=/usr/apache-ant-1.9.10
export PATH=$PATH:$ANT_HOME/bin
```

### 安装gitlab-runner
```bash
rpm -ivh gitlab-runner的安装包
```
此时会自动新建一个gitlab-runner用户，在/home/gitlab-runner  

注册runner：
```bash
gitlab-runner register # root用户执行
第一步输入项目的http地址
第二步输入项目的token
# 以上两个可在项目的setting->ci/cd->runner中找到，要用权限较高的gitlab用户去查看，如：root
第三步输入runner描述信息（随便写什么，建议写项目名）
第四步输入runner的标签名（随便写什么，建议写项目名）
第五步输入runner根据哪种命令执行（一般选shell）
正常此时runner会锁定到该项目并自动运行。
```

### .gitlab-ci.yml 配置
在项目的根目录添加.gitlab-ci.yml文件:
此时项目中有任何提交都会触ci功能。可在.gitlab-ci.yml文件中编辑对应的命令，runner会去逐条执行。项目会拉取到/home/gitlab-runner/builds/下对应的runner名称命名的目录中。

### 配置互信（可选）
在gitlab-runner用户中执行`ssh-keygen –t rsa` 命令
然后将id_rsa.pub中的内容复制到想要互信的服务器的用户中的authorized_keys中。（可通过ssh 用户名@服务器ip 命令去尝试是否互信成功）  
-scp war包的路径/war包名称.war 目标服务用户名@目标服务器ip地址:想传到的目录路径

ssh -t -t 用户名@ip地址 执行解压和部署命令，命令需写在“”中，用；区分（解压命令也可以在33机器上执行，然后把目录直接传到61机器里面）。

### 常见问题

**互信过程中可能出现的问题**：  
如果gitlab-runner用户进行了互信操作之后还是无法免密登录到其他服务器的普通用户，此时注意查看下需要登录的用户各级权限，用户目录-700 .ssh目录-700 authorized_keys-600.

**jsp无法同步的问题**：  
`cd /cib/domains/appdomain/servers/test/tmp/_WL_user/deploy/wlu333/jsp_servlet/_views/ ; rm -rf _jsp/`删除jsp页面的缓存，来达到同步  
上述命令也可以不用cd到指定目录并且直接指定目录。具体目录看对应的服务器。

**拉取问题**：
需要用对应项目成员的用户登录去触发ci功能（目前只有开发人员可触发执行拉取代码，不在项目内或者维护者用户无法拉取）。
root用户如果不在项目中执行会报错。

**jdk版本问题**：
runner默认用root用户的jdk去启动服务器，在编译的时候如果遇到jar包问题，则切换到runner用户修改java_home,且在对应的jdk中jre-lib-ext中添加servelt-api的jar包。

**runner安装包问题**：
需要和jdk的版本相匹配，el7的rpm包和el6的jdk可以注册成功但是runner是灰色无法运行（用root用户注册也不行）。
正常安装成功如果gitlab-runner用户注册仍无法运行，可以用root用户去注册runner。

**runner状态stuck问题**：
可能会出现runner脱机的问题，可在runner总页面将项目从runner上剔除，再重新添加。

**增量**
```bash
cd ../   # 到项目代码的目录
git checkout master 
git diff  HEAD^  --name-only | xargs  tar -zcvf diff.tar.gz
tar -zxvf diff.tar.gz

git diff HEAD^ --name-only > 任意路径/changelog.txt
```
**Sonar-scanner 代码扫描**
将安装包解压
配置：  
`/usr/local/sonar-scanner-4.2.0.1873-linux/conf/sonar-scanner.properties`
```
sonar.sourceEncoding=UTF-8
sonar.host.url=http://10.7.65.33:9000
sonar.jdbc.username=sonar
sonar.jdbc.password=sonar
sonar.jdbc.url=jdbc:postgresql://10.7.65.33/sonar
sonar.login=admin
sonar.password=admin
```
在/etc/profile 中配置对应的环境变量(示例)：
```bash
export SONARSCANNER_HOME=/usr/local/sonar-scanner-4.2.0.1873-linux/
export PATH=$PATH:$SONARSCANNER_HOME/bin
```
