###一、DOL的框架描述

　　DOL是一种能够自动将应用映射到多处理器SHAPES处理平台上的框架。包含三个部分：

 　1.DOL API:
 　　DOL定义了一系列计算和通信规则来为SHAPES平台激活分布平行的应用编程。通过这些规则，应用程序的编写者们可以编写程序，即使他们并不清楚底层架构的相关知识。
 　　
　 2.DOL功能型仿真
 　　为了给程序员一个测试他们应用的机会，功能型仿真框架应运而生。除了检查这些应用，框架还可以在应用层获取一些运行参数。
 　　
　 3.DOL最优化映射
 　　DOL最优化映射的目的在于计算一系列的最优映射来将应用映射到SHAPES处理平台上。首先，XML被允许来抽象描述应用和处理器。接着，所有的信息需要获得尽可能精确的估计。
 　　![这里写图片描述](http://img.blog.csdn.net/20161008205522484)

###二、DOL安装笔记
首先要使用虚拟机安装ubuntu，配置一些必要的环境。

sudo apt-get update
sudo apt-get install ant
 sudo apt-get install openjdk-7-jdk
sudo apt-get install unzip

下载dolethz.zip。

新建一个文件夹，路径可以自己选，记住就行：

mkdir dol

将dolethz.zip解压到新建的dol文件夹中：

unzip dol_ethz.zip -d dol

解压systemc：

tar -zxvf systemc-2.3.1.tgz

解压后进入systemc-2.3.1的目录下：

cd systemc-2.3.1

新建一个临时文件夹objdir：

mkdir objdir

进入该文件夹objdir：

cd objdir

运行configure，如果失败试试获取root权限：

../configure CXX=g++ --disable-async-updates

成功后显示如下信息：

![这里写图片描述](http://img.blog.csdn.net/20161008212132029)

编译systemc：

![这里写图片描述](http://img.blog.csdn.net/20161008212846779)

sudo make install

编译完后cd ..（注意.和d中间有空格）再ls得到文件目录如下：

![这里写图片描述](http://img.blog.csdn.net/20161008212545406)

输入pwd输出当前所在路径，如：

![这里写图片描述](http://img.blog.csdn.net/20161008212909201)

上图表明我当前的工作路径为/home/guanzhuoqun/systemc-2.3.1。

进入刚刚dol的文件夹：

cd ../dol

在build_zip.xml文件找到下面这段话：

![这里写图片描述](http://img.blog.csdn.net/20161008213238002)

把YYY改成之前pwd的结果，对于  64位 系统的机器，lib-linux要改成lib-linux64。

将下来执行：

ant -f build_zip.xml all

若成功会显示build successful：

![这里写图片描述](http://img.blog.csdn.net/20161008213513414)

接着进入build/bin/mian路径下：

cd build/bin/main

然后试着运行第一个例子：

ant -f runexample.xml -Dnumber=1

成功结果如图：

![这里写图片描述](http://img.blog.csdn.net/20161008213718363)

###三、感想和心得

　　这次实验的内容就是配置DOL，从一开始的盲目跟着教程去配置到不断通过遇到的问题来思考这些问题怎么解决，很多问题在教程中并没有解决方法，所以经常要和同学讨论交流以及上网搜索，在这个过程中学会了很多ubuntu的相关知识，特别是命令行的常见命令比如sudo su获取root权限等，同时也在潜移默化地吸收DOL的一些内容。