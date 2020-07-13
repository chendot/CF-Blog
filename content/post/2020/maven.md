
## 新建项目
新建maven项目 select from archetype

```bash
mvn archetype:generate -DgroupId=com.cj  -DartifactId=webAppDemo -DarchetypeArtifactId=maven-archetype-webapp -DinteractiveMode=false
```
意思就是我们通过archetype插件创建一个webapp项目，项目的groupId是com.cj，项目id是webAppDemo.使用的项目archetype是maven-archetype-webapp。也就是一个java web项目。interactiveMode= false，代表在执行过程中，用户不能进行输入操作。默认是true，需要用户进行操作。

## Ant 转 Maven


maven 安装目录

Bin:该目录包含Mvn运行的脚本

Boot：Maven自身的类加载器框架

Conf:包含非常重要的文件setting.xml

Lib：该目录包含了所有Maven运行时需要的Jave类库

Mvn help:system（该命令会打印出所有的Java系统属性和环境变量）

~/.M2  maven本地仓库