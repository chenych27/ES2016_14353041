###一、DOL实例分析和编程
####1、example1

　　要求修改example1，输出3次方数。
　　
  
　　生产者进程的功能是不断生成从1到LENGTH的数，然后传递给生产者的输出端口，通过通道投递到平方进程。
　　
  
　　平方进程相当于一个加工的模块，将生产者生成的数经过“加工”再传递到平方进程输出端口投递给消费者进程。本例子中的“加工”是将生产者传来的数进行平方。
　　
  
　　消费者进程对最后的结果进行处理，在本例子中是将平方模块传递来的值输出出来。
　　
  
　　这样一来，如何输出3次方数就一目了然，只要将平方模块中的输入输出转换公式ｉ＝ｉ＊ｉ改为ｉ＝ｉ＊ｉ＊ｉ即可。最后结果为：
　　
  
　　![这里写图片描述](http://img.blog.csdn.net/20161013005843261)
  
  
####2、example2


　　要求修改example2，使得3个square模块变为2个。
　　
  
　　上面分析的三个模块只是单纯的执行自己被定义的功能，但是将它们有机联合在一起的是样例对应的xml文件，它定义了这些模块之间是如何连接的。
  
  
　　在一个xml文件中，有process（进程）、sw_channel（通道）、connection（连接），一个通道对应两个连接。如果某一个部分有很多实例，那么可以迭代生成，如下图：
  
  
　　![这里写图片描述](http://img.blog.csdn.net/20161013005455166)
  
  
　　相当于一个循环，不断生成进程square，所以我们要实现题目的要求，只要令N等于2即可，N是一个值的名字，它的对应值在文件开始处：
  
  
　　![这里写图片描述](http://img.blog.csdn.net/20161013005735933)
  
  
　　改成2之后跑下程序，发现最后结果为i的4次方，修改正确。
  
　　
　　![这里写图片描述](http://img.blog.csdn.net/20161013005858355)
  
  
###二、DOL实例.dot文件展示
####1、example1
![这里写图片描述](http://img.blog.csdn.net/20161013010023996)
####2、example2
![这里写图片描述](http://img.blog.csdn.net/20161013010059231)
###三、实验感想
　　在这次实验中，学习了有关于生产者消费者模型的一个基础框架，理解了三个模块以及它们的连接逻辑，并在此基础上完成了这次实验。在实验中也遇到了一些小问题，就是如果要修改后跑出程序，就必须删掉整个build文件夹，再重新编译才可以。.dot文件需要用xdot来打开，所以需要安装该软件。
