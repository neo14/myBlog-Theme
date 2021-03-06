Title: Linux系统学习笔记：序  
Date: 2015-03-13 05:35:18  
Category: Linux系统学习笔记  
Tags: Linux  
Slug: linux-init  
Summary: Unix/Linux体系结构，Linux内核的主要模块，Linux的文件结构
# Linux系统学习笔记：序
*** 
&emsp;&emsp;Linux是一套免费使用和自由传播的类Unix操作系统，是一个基于POSIX和UNIX的多用户、多任务、支持多线程和多CPU的操作系统。它能运行主要的UNIX工具软件、应用程序和网络协议。它支持32位和64位硬件。Linux继承了Unix以网络为核心的设计思想，是一个性能稳定的多用户网络操作系统。
***
本人使用的Linux为Ubuntu，主要以《APUE》（第3版）为学习蓝本。
***
###  1. Unix/Linux 体系结构

如图:   
 ![](http://7xi2wq.com1.z0.glb.clouddn.com/linux_Architecture_of_the_UNIX_operating_system.png)  
内核的接口被称为系统调用。公用函数库构建在系统调用接口之上，应用程序既可以使用公用函数库，也可使用系统调用。Shell是一个特殊的应用程序，为运行其他应用程序提供了一个接口。
*** 
### 2. Linux 内核的主要模块
#### 2.1 进程调度 SCHED
进程调度指的是系统对进程的多种状态之间转换的策略。Linux下的进程调度有3种策略：  
	* SCHED_OTHER  分时调度策略  
	* SCHED_FIFO      实时调度策略，先到先服务   
	* SCHED_RR         实时调度策略，时间片轮转  

#### 2.2 内存管理 MMU
内存管理是多个进程间的内存共享策略。在Linux系统中，内存管理的主要概念是虚拟内存。

#### 2.3 虚拟文件系统 VFS
Linux支持多种文件系统，最常用的文件格式是ext2和ext3(ext4是ext3的改进版)，ext2文件系统用于固定文件系统和可活动文件系统，ext3在ext2的基础增加了日志功能。两者可以互相转换。

#### 2.4 网络接口
Linux支持多种网络接口和协议。网络接口分为网络协议和驱动程序，网络协议是一种网络传输的通信标准，而网络驱动则是对硬件设备的驱动程序。

#### 2.5 进程间通信
Linux操作系统支持多进程，进程之间需要进行数据的交流才能完成控制、协同工作等功能，Linux下的进程间的通信方式主要有管道方式、信号方式、消息队列方式、共享内存和套接字等方法。   

__(以上内容我将在操作系统和计算网络部分深入学习)__  
***  
### 3.  Linux的文件结构
一些常用目录的作用：   
1. /bin 包含了引导启动所需的命令或普通用户可能用的命令。  
2. /sbin 类似/bin，也用于存储二进制文件。其中的大部分文件多是系统管理员使用的基本的系统程序。  
3. /root 超级用户的目录。   
4. /lib 是根文件系统上的程序所需的共享库，存放了根文件系统程序运行所需的共享文件。这些文件包含了可被许多程序共享的代码，以避免每个程序都包含有相同的子程序的副本，故可以使得可执行文件变得更小，节省空间。  
5. /lib/modules 包含系统核心可加载各种模块，尤其是那些在恢复损坏的系统时重新引导系统所需的模块(例如网络和文件系统驱动)。  
6. /dev 存放了设备文件，即设备驱动程序，用户通过这些文件访问外部设备。比如，用户可以通过访问/ d e v / m o u s e来访问鼠标的输入，就像访问其他文件一样。  
7. /tmp 存放程序在运行时产生的信息和数据。但在引导启动后，运行的程序最好使用/ v a r / t m p来代替/tmp ，因为前者可能拥有一个更大的磁盘空间。  
8. /boot 存放引导加载器(bootstrap loader)使用的文件，如l i l o，核心映像也经常放在这里，而不是放在根目录中。但是如果有许多核心映像，这个目录就可能变得很大，这时使用单独的文件系统会更好一些。还有一点要注意的是，要确保核心映像必须在i d e硬盘的前1 0 2 4柱面内。  
9. /mnt 是系统管理员临时安装( m o u n t )文件系统的安装点。程序并不自动支持安装到/mnt 。/mnt 下面可以分为许多子目录，例如/mnt/dosa 可能是使用m s d o s文件系统的软驱，而/mnt/exta 可能是使用ext2文件系统的软驱，/mnt/cdrom 光驱等等。  
10. /opt 这里主要存放那些可选的程序。你想尝试最新的firefox测试版吗？那就装到/opt目录下吧，这样，当你尝试完，想删掉firefox的时候，你就可以直接删除它，而不影响系统其他任何设置。安装到/opt目录下的程序，它所有的数据、库文件等等都是放在同个目录下面。 举个例子：刚才装的测试版firefox，就可以装到/opt/firefox_beta目录下，/opt/firefox_beta目录下面就包含了运行firefox所需要的所有文件、库、数据等等。要删除firefox的时候，你只需删除/opt/firefox_beta目录即可，非常简单。  
11. /home 主要存放用户同名的目录，并且可以支持ftp的用户管理。  
12. /usr 是个很重要的目录，通常这一文件系统很大，因为所有程序安装在这里。/usr 里的所有文件一般来自linux发行版( distribution)；本地安装的程序和其他东西在/usr/local 下，因为这样可以在升级新版系统或新发行版时无须重新安装全部程序。/usr 目录下的许多内容是 可选的，但这些功能会使用户使用系统更加有效。/usr可容纳许多大型的软件包和它们的配置文件。下面列出一些重要的目录(一些不太重要的目录被省略了)。        
>    1. /usr/x11r6 包含xwindow系统的所有可执行程序、配置文件和支持文件。为简化x的开发和安装，x的文件没有集成到系统中。xwindow系统是一个功能强大的图形环境，提供了大量的图形工具程序。用户如果对microsoft windows或m achintos h比较熟悉的话，就不会对x window系统感到束手无策了。  
>	2. /usr/x386 类似/ usr/x11r6 ，但是是专门给x 11 release 5的。  
>	3. /usr/bin 集中了几乎所有用户命令，是系统的软件库。另有些命令在/bin 或/usr/local/bin 中。  
>	4. /usr/sbin包括了根文件系统不必要的系统管理命令，例如多数服务程序。  
>	5. /usr/man、/usr/info、/usr/doc 这些目录包含所有手册页、gnu信息文档和各种其他文档文件。每个联机手册的“节”都有两个子目录。例如： /usr/man/man1中包含联机手册第一节的源码(没有格式化的原始文件)，/usr/man/cat1包含第一节已格式化的内容。l联机手册分为以下九节：内部命令、系统调用、库函数、设备、文件格式、游戏、宏软件包、系统管理和核心程序。  
>	6. /usr/include 包含了c语言的头文件，这些文件多以. h结尾，用来描述c语言程序中用到的数据结构、子过程和常量。为了保持一致性，这实际上应该放在/usr/lib 下，但习惯上一直沿用了这个名字。
>	7. /usr/lib 包含了程序或子系统的不变的数据文件，包括一些site-wide配置文件。名字lib来源于库(library); 编程的原始库也存在/usr/lib 里。当编译程序时，程序便会和其中的库进行连接。也有许多程序把配置文件存入其中。  
>	8. /usr/local 本地安装的软件和其他文件放在这里。这与/usr很相似。用户可能会在这发现一些比较大的软件包，如tex、emacs等。  
    
13\. /var 包含系统一般运行时要改变的数据。通常这些数据所在的目录的大小是要经常变化或扩充的。原来/var目录中有些内容是在/usr中的，但为了保持/usr目录的相对稳定，就把那些需要经常改变的目录放到/var中了。每个系统是特定的，即不通过网络与其他计算机共享。 下面列出一些重要的目录(一些不太重要的目录省略了)。  
>	1. /var/catman 包括了格式化过的帮助(man)页。帮助页的源文件一般存在/usr/man/man中；有些man页可能有预格式化的版本，存在/ usr/man/cat中。而其他的man页在第一次看时都需要格式化，格式化完的版本存在/var/man 中，这样其他人再看相同的页时就无须等待格式化了。 (/var/catman 经常被清除，就像清除临时目录一样。)  
>	2. /var/lib 存放系统正常运行时要改变的文件。  
>	3. /var/local 存放/usr/local 中安装的程序的可变数据(即系统管理员安装的程序)。注意，如果必要，即使本地安装的程序也会使用其他/var 目录，例如/var/lock。  
>	4. /var/lock 锁定文件。许多程序遵循在/var/lock 中产生一个锁定文件的约定，以用来支持他们正在使用某个特定的设备或文件。其他程序注意到这个锁定文件时，就不会再使用这个设备或文件。  
>	5. /var/log 各种程序的日志( log )文件，尤其是login (/var/log/wtmp log纪录所有到系统的登录和注销) 和syslog (/var/log/messages 纪录存储所有核心和系统程序信息)。/var/log 里的文件经常不确定地增长，应该定期清除。   
>	6. /var/run 保存在下一次系统引导前有效的关于系统的信息文件。例如， /var/run/utmp 包含当前登录的用户的信息。  
>	7. /var/spool 放置“假脱机( spool )”程序的目录，如mail、news、打印队列和其他队列工作的目录。每个不同的spool在/var/spool 下有自己的子目录，例如，用户的邮箱就存放在/var/spool/mail 中。  
>	8. /var/tmp 比/tmp 允许更大的或需要存在较长时间的临时文件。注意系统管理员可能不允许/var/tmp 有很旧的文件。  

