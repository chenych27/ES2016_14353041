#### 一、配置Ubuntu的软件源

根据下面这个链接配置即可（一般而言，这些配置都是默认的）：

https://help.ubuntu.com/community/Repositories/Ubuntu

配置成下图所示即可：

![这里写图片描述](http://img.blog.csdn.net/20161111115535598)

####二、添加软件源到sources.list

添加软件源是为了让操作系统知道去哪里下载程序，并根据命令自动安装软件。

![这里写图片描述](http://img.blog.csdn.net/20161111120017484)

之后会让你输入密码，输入即可：

![这里写图片描述](http://img.blog.csdn.net/20161111120147428)

####三、设置密钥

![这里写图片描述](http://img.blog.csdn.net/20161111120250597)

结果如下图所示：

![这里写图片描述](http://img.blog.csdn.net/20161111120350304)

####四、安装
首先确认你的Debian的软件包索引是最新的。

![这里写图片描述](http://img.blog.csdn.net/20161111120526475)

在ROS中有许多不同的函数库和工具，建议是完全安装，也可以根据自己的要求分别安装。
完全安装时的工具包括ROS, rqt, rviz, robot-generic libraries, 2D/3D simulators, navigation and 2D/3D perception。

![这里写图片描述](http://img.blog.csdn.net/20161111120702914)

####五、初始化rosdep
rosdep能够使你更方便安装一些系统依赖程序包，同时ROS的一些主要部件的运行也需要rosdep。

![这里写图片描述](http://img.blog.csdn.net/20161111121516076)

####六、设置环境
添加ROS的环境变量，这样，当你打开你新的命令行时，你的bash会话中会自动添加环境变量。

![这里写图片描述](http://img.blog.csdn.net/20161111121758671)

如果你只想改变当前shell的环境变量，可以执行下面的语句：

![这里写图片描述](http://img.blog.csdn.net/20161111121904353)

这些语句都不会有很多反馈，结果很清晰：

![这里写图片描述](http://img.blog.csdn.net/20161111122005480)

####七、安装rosinstall
rosinstall命令是一个使用的非常频繁的命令，使用这个命令可以轻松的下载许多ROS软件包。

![这里写图片描述](http://img.blog.csdn.net/20161111122142998)

####八、创建ROS工作环境

运行：

![这里写图片描述](http://img.blog.csdn.net/20161111122517986)

这时在src文件夹中可以看到一个CMakeLists.txt文件，即使这个工作空间是空的（在src中没有package），仍然可以建立一个工作空间。

![这里写图片描述](http://img.blog.csdn.net/20161111122710924)

下一步执行：

![这里写图片描述](http://img.blog.csdn.net/20161111122754612)

catkin_make命令建立一个catkin工作空间，这时候在catkin_ws目录下可以看到三个文件夹：

![这里写图片描述](http://img.blog.csdn.net/20161111123127900)

在devel文件夹中可以看到许多个setup.*sh文件。

![这里写图片描述](http://img.blog.csdn.net/20161111123459115)

先启动你的新的setup.*sh 文件。

![这里写图片描述](http://img.blog.csdn.net/20161111123539677)

为了确认你的环境变量是否被setup脚本覆盖了，可以运行一下命令确认你的当前目录是否在环境变量中：

![这里写图片描述](http://img.blog.csdn.net/20161111123707752)

输出结果：

![这里写图片描述](http://img.blog.csdn.net/20161111123808241)

至此环境就建立好了。Cartographer是Google开源的一个SLAM算法，接下来就来体验一下。

####九、安装所有依赖项

如下图所示一步步实现即可：

![这里写图片描述](http://img.blog.csdn.net/20161111213552919)

####十、安装ceres solver

安装路径是随意的，自己记住就好。

1.      git clone https://github.com/hitcm/ceres-solver-1.11.0.git

2.      cd ceres-solver-1.11.0

3.      mkdir build
     
4.      cd build

5.      cmake ..

6.      make –j3

7.      sudo make install

####十一、安装 cartographer

1.       回到主目录，git clone https://github.com/hitcm/cartographer.git

2.       cd cartographer/build

3.       cmake .. -G Ninja

4.       ninja       //这一步会比较漫长

5.       ninja test

6.       sudo ninja install

####十二、安装cartographer_ros

1.   主目录下执行：mkdir catkin_ws

2.  cd catkin_ws

3.  wstool init src

4. cd src

5.  git clone https://github.com/hitcm/cartographer_ros.git

6. cd ..

7. catkin_make

这个时候catkin_ws目录下文件夹有：

![这里写图片描述](http://img.blog.csdn.net/20161111215022892)

####十三、测试

在windows下下载2D数据：

https://storage.googleapis.com/cartographer-public-data/bags/backpack_2d/cartographer_paper_deutsches_museum.bag

然后拷贝到虚拟机，放的目录要记住。然后运行：

![这里写图片描述](http://img.blog.csdn.net/20161111215422436)

记住根据自己放文件的路径修改home后面的相关路径。

在这里会有可能报错：

![这里写图片描述](http://img.blog.csdn.net/20161111215830294)

这个时候尝试：

![这里写图片描述](http://img.blog.csdn.net/20161111220051064)

在运行一次，软件打开，出来一个2D动画，截一张图：

![这里写图片描述](http://img.blog.csdn.net/20161111220324832)

####十四、实验总结

这次实验比较麻烦，主要是配置过程会遇到各种各样的问题，比如make-j会导致虚拟机崩溃重启等等，还有最后的软件都打开了，但是却无法正常显示画面，这些都是因为在实验过程中有些东西没有配置好的缘故，比如无法正常显示画面就是因为在配置的时候没有配好ninja的缘故，当时那里等的比较久，所以在318/327的时候虚拟机休眠中断了配置，当我重新打开的时候，继续下一步，所以配置不完整，从而导致最后的失败。这样的失败有很多，但是在每次失败的时候，通过询问同学和网络搜索都能找到相应的解答，最终还是顺利完成了实验，做出来的时候就像生了个孩子，如释重负。