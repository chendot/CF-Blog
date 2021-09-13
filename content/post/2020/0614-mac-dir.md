---
title: "MacOS 文件目录"
date: 2020-06-14
sidebar: false
tags:
  - "IT"
  - 转载
categories:
  - "技术文档"
---

打开Macintosh HD你会发现内中有四个文件夹(一般情况下，隐藏文件夹是不可见的，而且，可能会更多，比如安装xcode后会有developer文件夹). 

分别有——应用程序(Applications)、系统(System)、用户(User)、资料库(Library)。四个文件夹中又分别各有若干数量的文件夹存在。
<!--more-->
 

Applications：这个当然就是存放各种软件的位置了。

 

System:包含由Apple安装的系统软件。这此资源是系统正常运行所必须的，位于启动卷宗中，在该区域中，用户不允许添加、删除或更改这些资源。

            /System/Library/CFMSupport CFM, Code Fragment Manager, 等同旧Mac OS应用程序都会使用的共有程式库. 以确保Mac OS环境的一致性. 当中储存有一个在OS X中极为重要的档桉---CarbonLib, 是执行炭火软件时必不可欠的档桉. 此外还有DiscRecordingLib(CD/R-RW用的程式库), OpenGLLib(OpenGL), stbCLib(C语言), TWAINSourceManager.Shlb(TWAIN对应), vecLib(AltiVec)等程序库, 都是储存于此.

            /System/Library/DTDs 作为存放系统所使用的各种XML档桉, 并为其格式定义之档桉. Mac OS X Data形式製成的文书, 分别由三个档桉管理, 分别是PropertyList.dtd, KeyboardLayout.dtd及sdef.dtd三个档桉所组成. 而DTD, 全名为Document Type Definition. 此外, .plist档桉亦是由XML撰写出来的.

            /System/Library/Extensions 其实这裡就是用作存放硬件驱动的地方, 苹果不称驱动程序为driver, 而是称为Extension.

            /System/Library/Filesystems 主要就是用以存放OS X对应及支持何种档桉格式的资料. 例同标准的AppleShare(苹果档桉分享标准), ISO 9660/FTP/HFS及至网络上用的如Samba等

            /System/Library/HelpViewer 一切和Mac OS Help有关的档桉及文件都存放于此

            /System/Library/Find 就是搜寻机能了. 是对应多国语言的.

            /System/Library/OpenSSL 全名为Secure Sockets Layer. 是一套通讯加密技术, 一般用于Web服务器上, 会将密码传送时以加密的暗号处理, 从而减低第三方成功盗 取资料的可能. 一般应用于以https开首的URL上. Mac OS X内置的Web Server---Apache, 亦包含这个服务.

            /System/Library/CoreServices/Dock这是OS X的特徵之一, 这部份是有关Dock的资料

            /System/Library/CoreServices/Finder.app这个比较特别, 因为这是一个应用而非一个档桉夹, Finder.app可说是负责掌控整个OS上的一切资源.

            /System/Library/CoreServices/Kerberos由MIT(麻省理工大学)开发的网络认证技术. 能够很简单地以单一ID登入系统的检证技术. Mac OS X支援其版本4的Kerberos. 所谓Kerberos, 在希腊神话中是一头住在冥界, 拥三头, 蛇尾的地狱守门犬

            /System/Library/CoreServices/Menu ExtrasStatus bar上面所有系统自带工具的原文件，双击打开可以直接在status bar上添加相应文件

            /System/Library/CoreServices/Setup Assistant所有有关设定助理的资料都存放于此.

            /System/Library/CoreServices/Software Update这裡就是负责Software update的地方

 

Library：系统资源，比如字体、ColorSync 配置、偏好设置以及插件都应该安装在 Library 目录下适当的子目录中。

            Application Support包含了应用相关的数据以及支持文件，比如第三方的插件，帮助应用，模板以及应用使用到但是并不需要用来支持运行的额外资源文件。按照惯例，所有这些内容都会被存储在以应用名称命名的子目录当中。

            Assistants包含了帮助用户进行配置或者其它任务的程序。

            Audio包含了音频插件以及设备驱动。

            Caches包含了可以根据需要重新生成的缓存数据。应用永远都不能依赖于缓存文件的存在。缓存文件应该存储在目录名称域应用包的标识相匹配的目录当中。 缓存文件还可以进而根据需要划分为用户或者会话专用的子目录。(参考Mac OS X 文档中的多用户环境 )

            ColorPickers包含了用来选择色彩的资源，它们根据某种模型，比如 HLS (色彩角、饱和度、亮度) 选择器或者 RGB 选择器。

            ColorSync包含了 ColorSync 配置和脚本。

            Components包含了系统包和扩展。

            Contextual Menu Items包含了用于扩展系统级菜单的插件。

            Dictionaries包含了系统自带的字典文件。

            Desktop Pictures桌面图片目录。

            Documentation包含了供计算机用户和管理员参考的文档文件和 Apple 帮助包。(Apple 帮助包在Help 子目录当中。) 在本地域中，这个目录包含了 Apple 公司发布的帮助包(不包括开发者文档)。

            Extensions包含了设备驱动和其它内核扩展。(只存在于系统域当中。)

            Favorites包含了指向经常访问的文件夹、文件或者网站的别名。(仅仅存在于用户域当中。)

            Fonts包含了用于显示和打印的字体文件。

            Frameworks包含了框架和共享库。系统域中的 Frameworks 目录仅仅用于 Apple 公司提供的框架。开发者需要把他们自己定制的框架安装在本地域或者用户域中。

            Image Capture储存有多个DC厂商的标准驱动程序, 当中还细分有两个档桉夹, 其中Devices中, 苹果将各款不同DC细分成8个种类不同的驱动. 此外, 这裡还存放了各种和相机, Scanner有关的驱动, 例同PTP(Picture Transfer Protocol), TWAIN等.

            Input Methods包含了安装的输入法

            Internet Plug-ins包含了 web 浏览器内容所需要的插件、库和过滤器。

            iTunes第三方的iTunes的插件及库

            Java包含了Java运行环境。

            Keyboard Layouts包含了键盘定义。

            Keychains包含了钥匙串文件。

            Logs包含了控制台和系统服务的日志文件。用户也可以利用控制台应用浏览这些日志。

            Mail包含了信箱文件

            Modem Scripts调制解调器脚本，也就是猫的驱动了。

            Perl Perl程序的功能扩展及库，比如Cocoa Conler就需要这个功能。

            PreferencePanes包含了系统参数应用的插件。可以找到系统偏好设置里的对应项。

            Preferences包含了用户参数设置。有关用户参数的信息请参考运行时刻配置指南 。

            Printers在系统和本地域中，该目录包含了打印机驱动，PPD 插件和用来配置打印机的库。在用户域当中，该目录包含了用户可用的打印机配置。

            QuickLook包含了快速查看插件。

            QuickTime包含了 QuickTime 组件和扩展。

            Receipts安装过的.pkg安装包的替身，但不是.pkg安装包本身。例如系统升级或安装时的.pkg。或vpc安装时的.pkg包。

            Screen Savers包含了屏幕保护程序。

            Scripting Additions包含了对 AppleScript 的功能进行扩展的脚本和脚本资源。

            Services（只存在与个人文件夹中）包含了服务的脚本文件

            Scripts包含了各种程序所需要的脚本文件

            Sounds（只存在于个人文件夹中）包含了系统告警声音。

            Speech包含了语音的相关资源文件。

            Spelling包含了拼写的配置文件。

            StartupItems包含了在系统导入时刻运行的系统以及第三方脚本和程序。 (更多有关系统导入时刻启动步骤的信息请参考系统启动程序主题 )

            User Pictures用户账号中，用户显示的图片的文件。

            Updates包含了系统自动更新的安装文件。默认会自动删除里边的文件。

            Web Server包含了 web 服务器内容。本目录包含了 web 服务器使用的 CGI 脚本和网页

            Widgets包含了已安装的Widget小工具

 

User：包含了某个用户专有的资源。这里也有一个Library文件夹，不同与上边的那个Library，是专为你的帐号服务，里面放的是你自己的个性化字体、配置文件等

             Applications包含仅仅当前用户可用的应用。

             Desktop 包含了 Finder 在当前登录用户桌面上显示的桌面项。

             Documents 包含了用户的个人文档。

             Download 包含了下载的各种文档。

             Library 包含了应用设置、偏好设置一起其他用户专有的系统资源

                       Application Support包含了应用相关的数据以及支持文件，比如第三方的插件，帮助应用，模板以及应用使用到但是并不需要用来支持运行的额外资源文件。按照惯例， 所有这些内容都会被存储在以应用名称命名的子目录当中。

                       Assistants包含了帮助用户进行配置或者其它任务的程序。

                       Audio包含了音频插件以及设备驱动。

                       Caches包含了可以根据需要重新生成的缓存数据。应用永远都不能依赖于缓存文件的存在。缓存文件应该存储在目录名称域应用包的标识相匹配的目录当 中。缓存文件还可以进而根据需要划分为用户或者会话专用的子目录。(参考Mac OS X 文档中的多用户环境 )

                       ColorPickers包含了用来选择色彩的资源，它们根据某种模型，比如 HLS (色彩角、饱和度、亮度) 选择器或者 RGB 选择器。

                       ColorSync包含了 ColorSync 配置和脚本。

                       Components包含了系统包和扩展。

                       Contextual Menu Items包含了用于扩展系统级菜单的插件。

                       Dictionaries包含了系统自带的字典文件。

                       Desktop Pictures桌面图片目录。

                       Documentation包含了供计算机用户和管理员参考的文档文件和 Apple 帮助包。(Apple 帮助包在Help 子目录当中。) 在本地域中，这个目录包含了 Apple 公司发布的帮助包(不包括开发者文档)。

                       Extensions包含了设备驱动和其它内核扩展。(只存在于系统域当中。)

                       Favorites包含了指向经常访问的文件夹、文件或者网站的别名。(仅仅存在于用户域当中。)

                       Fonts包含了用于显示和打印的字体文件。

                       Frameworks包含了框架和共享库。系统域中的 Frameworks 目录仅仅用于 Apple 公司提供的框架。开发者需要把他们自己定制的框架安装在本地域或者用户域中。

                       Image Capture储存有多个DC厂商的标准驱动程序, 当中还细分有两个档桉夹, 其中Devices中, 苹果将各款不同DC细分成8个种类不同的驱动. 此外, 这裡还存放了各种和相机, Scanner有关的驱动, 例同PTP(Picture Transfer Protocol), TWAIN等.

                       Input Methods包含了安装的输入法

             Movies 包含了 QuickTime 以及其它格式的数字影片。

             Music 包含数字音乐文件 (.aiff、.mp3、.m4p 及其它格式)。

             Pictures 包含各种格式的图像文件。

             Public 包含了用户需要和其他用户共享的内容。缺省情况下，其他用户可以访问这个目录。

             Sites 包含了用户个人网站的网页。如果需要其他用户能够访问这些网页，需要使能 Web 共享。

 

～～～硬盘中还有几个隐藏文件夹～～～

1)     bin---------储存有基本的UNIX指令

2)     sbin--------UNIX 系统指令的储存地方, 是比较进阶的指令

3)     etc---------系统设定档桉储存地方

4)     var---------改动频繁的档桉, 都置放于此, 例如各log档桉

5)     tmp--------系统的暂存档

6)     usr---------UNIX的使用者专用档桉夹

 

MAc OS X系统深入了解－－系统文件结构篇

 

OS X采用的是类UNIX的多用户系统。

通常我们在启动盘下面都只能看到应用程序、资源库、系统、用户这４个目录。但其实还有很多的隐藏目录，如bin、sbin之类的，这些都是系统的一些资源，一般是不用普通用户去访问，是些比较重要的系统文件及配置文件。

所以我这里就只是探讨一下通常在Finder中可以触及的文件项目和资源。

 

首先我们来了解一下OS X系统的几大组成部分：

文件系统区域：

作为了一个多用户的操作系统，控制系统资源的访问对于保证系统的稳定性是非常重要的。通过目录的设置，由当前用户的操作权限来决定该用户对每部分资源的访问。

在OS X系统中，存在以下４个文件系统区域：

User:这个区域包含了登录到系统的用户可供使用的特定资源。该区域由用户的主目录来定义，在这个区域中，用户具有完全的控制权限。

Local: Local区域包括如文件、程序这些被系统中所有用户共享的资源，但它不是系统运行所必须的。Local区域没有一个相应的单独的目录，它包含于启动卷宗的多个目录中。具有系统管理员权限的用户可以添加、删除或修改此区载的项目。

Network:此区域包含了本地局域网中可被所有用户共享的资源，如文件或应用程序。该区域的代表项目在网络文件服务中的位置，并受网络管理员的控制。

System:包含由Apple安装的系统软件。这此资源是系统正常运行所必须的，位于启动卷宗中，在该区域中，用户不允许添加、删除或更改这些资源。

 

用户区域包含指定给一个单独的用户的资源。由当前用户的个人目录来表示。每个Mac OS X系统用户必须有一个账号，在文件系统中给每个用户账号指定一个目录空间。目录中包括了用户的应用程序、资源以及文档。用户个人目录以用户账号的短名称来命名，并且是唯一的。

用户区域可以让用户为自己定义一个合理的工作环境，当用户登录时，Finder将恢复用户的工作环境，并按预置设置为用户上次使用时的状态。同样的，应用程序及其它系统软件按程序预置、网络设置、email设置、字体设置及其它设置来进行恢复。

用户的个人目录的位置依赖于用户的账号。如果用户账号是本地账号，那么用户的个人目录则位于启动卷宗的"User"目录中，如果是一个网络账号，则个人目录位于网络服务器中。

无论用户的个人目录实际位置在哪里（实际上，我们还是可以通过终端命令更改个人目录的实际位置的），OS X都使用"~"字符来代表当前登录用户的个人目录。这个符号可以与其它路径来组合使用。

 

表一：

~ 当前用户目录的顶级目录，相当于"/User/当前用户名"这个目录

~/Library/Fonts 当前用户个人目录中的字体储存位置

~Steve 用户Steve的个人目录。

说明：这里我们需要注意的是，终端或系统中，我们其实都可以多重登录的，因此，在使用"~"的时候，连接的是“当前登录用户“的个人目录。所以，当你登录为不同的用户时，"~"所指的位置并不相当。

 

表二：

这里我们列出的是个人目录下一些常见的目录：

Applications 包含一些只有当前用户可以使用的程序，比如我们安装了一个程序，安装时选Applications，应用程序将会默认安装到这里！

Desktop：包含当前用户显示在Finder桌面上的所有项目。

Documents：用户个人的一些文档。经常会包含一些程序使用的文件或者下载的文件，以及程序安装的纪录文件。

Library：包括应用程序设置、预置及其它用户指定的系统资源或设置。

Movies：QuickTime或其它格式的影片

Music：数字音乐文件（如.aiff, .mp3, .m4p或其它格式)，包括iTunes自动倒入的歌曲。

Pictures：图片文件，包括iPhoto自动导入的数码相机中的图片

Public：你可以把需要与其它用户共享的文件放在这个目录中，默认状态下，这个目录可以被其它所有用户访问。

Sites：用户的个人站点网页文件。在被其它用户访问之前，你必须在“系统预置－共享-Web共享“中打开共享。

当新建账号时，"Applications"目录并不会自动添加到该用户的个人目录中。用户可以自已手工建议一个"Applications"，并把自己的程序放在该目录中，系统会自动搜索该目录中的项目。

在'/User'目录中包含一个叫"Shared"的子目录，这个目录可以被本地的所有用户访问（不过请不要把应用程序放置在该目录中），所有用户都可以从该目录中读取或写入文件，用于本地用户的文件交换及共享。

 

本地区域包括本地计算机所使用的资源，但它不是系统运行所必须的。比较典型的包括：应用程序、实用工具、自定义字体、自定义的启动项目以及应用 程序全局设置。在"Applications" 以及 "Library"目录中也包含了部分资源，这些资源仅代本地用户使用，而网络用户则无法访问。

如果希望本地所有用户共享资源，那么系统管理员可以安装资源到本地区域，苹果公司开发的应用程序都安装在"/Applications" 及 "/Applications/Utilities "目录中，第三方的程序及工具也可以安装在这些目录中。其它的系统资源，如字体、预置以及插件放置在"/Library"相应的子目录中。

 

网络部分

网络区域包括本地局域网中的的资源。网络用户可以访问程序、文档以及其它资源，包括AplleShare及 Web共享。

 

表三：

/Network/Applications 包括可以被本地局域网中其它用户运行的一些应用程序。

/Network/Library 包含如：插件,音频文件, 文档, 框架, 色彩,及字体这些供本地局域网用户使用的资源.

/Network/Servers 包含本地局域网中提供的NFS文件服务的连接

/Network/Users/ 包括所有本地网用户的个人目录。这是个人目录默认的位置。个人目录也可以存储在其它服务器中。

 

系统区域

系统区域包括了Mac OS X运行所必须的资源，它全部位置于启动盘的"/System"目录中。这些资源由苹果公司提供并只有'root'用户可以修改其内容。管理员用户以及程序将不会安装任何资源在这个目录或直接修改其内容。

默认时，"/System"仅包括一个"Library"子目录，这个子目录包含了许多与其它Library目录相同类型的资源。

请不要手工添加、删除或者修改此目录的资源，否则有可能导致系统无法正常启动。

 

Library目录

Library目录被用来存储程序及系统特殊资源的一个特殊目录。每个文件系统都有它自己的Library目录。通常，程序可以用它来存储内部数据或临时文件，但不会存储程序本身或用户的数据文件。

它包括很多标准的子目录，系统通常会认为已经存在这些标准的。所以请不要删除Library中的子目录。当然，程序也可以创建新的子目录来储存程序的特殊数据。

Library可以位于启动盘根目录及用户的个人目录中。虽然位置不同，内容及作用大体相同。

唯一的区别就在于：根目录下的Library是本机所有用户的共同设置，而个人目录中的Library则只是该用户的设置。

下面我们将列出在Library常见的一些子目录，你可以通过这个说明来了解这些目录到底有何用途。从而来决定你要作什么。

 

Library目录中的子目录：

Application Support ：包括程序的特殊数据以及支持文件，如第三方插件，帮助程序、模板以及被程序使用但不允许操作的附加资源。通常所有的项目都放置在以程序命名的目录中。例 如Adobe公司的程序，都将放在名叫“Adobe“的子目录中，而苹果公司的程序支持则放置在“Apple“这个子目录中。

Assistants：包括程序用来帮助用户设置或完成其它任务的资源。

 

Audio：包括音频插件及设备驱动。

Caches：再生所必须的缓存数据。

ColorPickers：采集色彩时所依赖的模式的资源。例如HLS或RGB。

ColorSync：色彩管理预置及脚本。

Components：系统组织和功能扩展。

Contextual Menu Items：附加的系统级关联菜单插件，如阿拉丁的解压缩关联菜单、iGetter的关联菜单。

Desktop Pictures：桌面图片目录。

Documentation：文档及用户和管理员使用的苹果帮助文件包(也有的在"Help子目录中")。

Extensions：包括设备驱动及其它核心功能。类似于OS 9下的"功能扩展"目录。

Favorites：包括经常访问的目录、文件或网站的替身，仅存在于个人目录的库目录中。

Fonts:显示和打印用的字体文件

Frameworks：框架和共享的资源库，开发者可能会安装自己的框架或资源在该目录中。

Image Capture：通常是扫描仪的驱动。

InputManagers：输入法管理，

Internet Plug-ins：网络浏览器使用的插件、库及过滤器。如Flash插件、Realplayer插件。

iTunes：第三方的iTunes的插件及库，

Java：如果你安装了Java，那么就会有这个目录，包括了Java的一些功能扩展及其它资源。

Keyboard Layouts：键盘布局

Keychains：系统中各个钥匙串的内容。

Logs：控制台及系统服务的记录文件，你可以通过：应用程序－实用程序－控制台来查看。

Modem Scripts：调制解调器脚本，也就是猫的驱动了。

Mail：用户的电子邮件内容，这只存在于每个用户的个人目录的库目录中。

Perl：Perl程序的功能扩展及库，比如Cocoa Conler就需要这个功能。

Plug-ins：系统插件，比如磁盘工具的磁盘映像。

PreferencePanes：系统预置插件，一般显示在系统预置的最下方。如安装阿拉丁解压缩软件时生成的StuffIt AVR.prefPane

Preferences：预置目录，包括系统、应用程序及用户的各种设置。通常如果预置文件损坏，会导致程序或系统的操作失常，这个时候可以通过删除相应的预置来尝试解决问题。

Printers：打印机驱动。PPD插件，以及配置打印机所需要的库文件。

QuickTime：QuickTime的插件及功能扩展。

Receipts：安装过的.pkg安装包的替身，但不是.pkg安装包本身。例如系统升级或安装时的.pkg。或vpc安装时的.pkg包。

Screen Savers：屏幕保护文件。

Scripting：AppleScript附加的脚本及脚本资源。

Sherlock Plug-ins：Sherlock兼容的插件及功能扩展。

Sounds：系统警告提示音

StartupItems：系统运行时自动启动的系统及第三方脚本或程序。一般通过系统预置－账号来进行设定。

User Pictures：用户账号中，用户显示的图片的文件。

WebServer：Web服务内容。也就是个人Web共享的内容。包括CGI脚本及网页文件。网页文件放置在Documents子目录中。

 

文件系统

从体系结构上看，Mac OS X实现了对多文件系统的支持，其中最为重要的文件系统包括有：Mac OS Extended (HFS+)，Mac OS Standard (HFS)，UFS， ISO 9660， NFS和 AFP。但从用户的角度看，文件系统又是单一的。当用户复制，移动或拖移文件和文件夹时，（会感觉似乎）只存在一个文件系统。

文件系统如何被组织

    Mac OS X文件系统中的几乎每个文件都有其适合放置的存储这一类型文件的标准目录区域。而对用户来说，这并不意味着他们就必须把应用程序和应用程序资源放在被推荐 的区域。由于应用程序最终会被打包，因此无论他们被安装在哪里，都能满足自身要求。但假如用户没有把某些内容放在系统软件期望的位置。他们有可能会丧失 Mac OS X的一些优势。例如，Finder首先通过搜索应用程序的标准位置来导入应用程序数据库（见“收集应用程序信息”一节）。一旦这样做，结果有可能会造成一 个隶属于某个应用程序（但不在那一区域）的文档，不能在双击时被立即打开。

文件系统的层次通常被表现为一个以“根（root）”开始的分层结构，在典型的Mac OS X文件系统的根目录中（“根”用起始的“/”符号来表示），它包含以下项目：

/Mac OS X/--一个特殊的卷，操作系统由它开始启动，系统文件和资源也被安装在其上。这个卷通常是一个被格式为Mac OS扩展格式（HFS+，Mac OS Extended）的卷（虽然它也可以是UFS卷）。名称“Mac OS X”是它默认的卷名，但用户也可以修改它。

/Network/--作为装载到用户系统上的本地网络的根目录。无论用户是否连接到网络上，/Network/目录（其图标是一个“地球”）将始终出现。

/OtherVolumes/--显示一个或多个被连接的外部设备或不是启动卷的内部设备。其中可以包括有Zip驱动器，CD-ROM驱动器， 数码相机，被装载的网络服务器以及硬盘和它们的分区等。（“OtherVolumes”只是一个真实名称的代表，被连接的卷的实际名称将会是不同的）。

所有非启动卷在它们被装载时出现，被卸载时消失。对此有一个例外，用户的iDisk卷即使在被卸载后也不会消失。

卷的物理结构与Finder向用户所显示的略有不同。假如用Terminal程序看一下目录结构，您会看到启动卷被装载在根目录层（/），而非 启动卷被放在/Volumes/目录中。Finder提供了这种抽象方式，用来在基本的UNIX 系统上提供一个更加传统的Mac OS界面。

像/usr, /bin和/etc等目录都是标准的BSD目录，它们也存在于根目录层，但Finder向用户隐藏了它们。

系统域

系统域包含了要求由Mac OS X来运行的资源。系统域中的所有资源被放置在启动卷上的/System目录下。这些资源由Apple提供，只有root用户可以修改这个目录的内容。管理用户和应用程序不能在系统域中安装资源或是直接修改它的内容。

默认情况下，/System目录仅包含了一个Library子目录。与系统中的其他Library目录一样，这个子目录中包含了许多相同类型的 资源。然而在系统域中，这个目录还包含了构成Mac OS X系统的许多核心服务，框架和应用户程序。关于Library目录的更多信息，请参见“Library 目录”一节。

 

——————————————————————

Library目录

 

Library是一个特殊的目录，用于存储特定的应用程序和特定的系统资源。每个文件系统域都有其自身Library目录的副本，这些 Library目录具有不同的访问级别以匹配不同的域类型。虽然一个应用程序可以使用这个目录来存储内部数据或临时文件，但将应用程序的束自身或是用户数 据文件存放在Library目录中将是不足取的。应用程序的束应放在一个/Applications目录中，而用户数据应放在用户的home目录中。

 

Library包含了许多标准的子目录。系统例程要求许多标准子目录必须存在，因此删除Library的子目录决不是一个好主意。然而，当需要存储特定的应用程序数据时，应用程序可以创建一个新的子目录。

 

Application Support

特定应用程序的第三方插件，帮助程序，模板和其他资源。按规定，这些项目应被放置在以应用程序命名的子目录中。举个列子，应用程序MyApp的第三方资源将被放在Application Support/MyApp/中。注意，一个由应用程序开发者创建的资源应被放置在自己的应用程序包中。


---

在计算中使用的脚手架指的是两种技术之一：第一种是与某些MVC 框架中的数据库访问相关的代码生成技术; 第二种是由各种工具支持的项目生成技术。

脚手架是一种由一些 model–view–controller 框架支持的技术，程序员可以在其中指定应用程序数据库的使用方式。该编译器或框架使用说明书中，与预先定义的代码模板在一起，产生最终代码的应用程序可以使用它来创建，读取，更新和删除数据库条目，有效治疗模板作为“ 支架 ”上建立更强大的应用程序。 (维基百科)

---

就是由“程序员手写代码”跨越到了“程序员指挥机器自动生成代码”的时代~~ 并且利用脚手架，我们可以爬到更高的地方、建更高的楼房


占用cpu
windowServer
kernel_task
Code Hepler
sysmond

java

内存占用
WPS Office service
360Chrome Helper