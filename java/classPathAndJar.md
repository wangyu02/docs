# classpath 和 jar

1. 概念辨析 -- 什么是classPath?

   classPath 是jvm用到的一个环境变量，用来只是JVM如何来搜索class，classPath的本质就是一组目录的集合，它设置的搜索路径与操作系统相关。

2. 为什么要设置classPath？

   java是编译型预言，源码文件是.java，而编译后的.class文件才是真正可以被jvm执行的字节码，因此需要让JVM知道，如果要加载一个abc.xyz.hello的类，应该去哪搜索对应的Hello.class文件

3. classPath 设定的两种方式：

   - 在系统环境变量中设置classPath环境变量，不推荐使用
   - 在启动JVM的时候设置classPath变量，推荐使用
   
4. 所述：

   - JVM通过环境变量classPath决定搜索class的路径和顺序
   - 不推荐设置系统环境变量`classpath`，始终建议通过`-cp`命令传入；
   - jar包相当于目录，可以包含很多`.class`文件，方便下载和使用；
   - `MANIFEST.MF`文件可以提供jar包的信息，如`Main-Class`，这样可以直接运行jar包。

