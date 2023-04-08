# FastDFS

属于分布式文件系统，是一个软件，用于管理分布式的文件服务器上的文件。

FastDFS 文件系统由两大部分构成， 一个是客户端， 一个是服务端 。

客户端通常指我们的程序， 比如我们的 Java 程序去连接 FastDFS、操作 FastDFS，那我们的Java程序就是一个客户端。FastDFS文件系统Java客户端是指采用 Java 语言编写的一套程序，专门用来访问 fastDFS文件系统， 其实就是一个 jar 包。  

服务端由两个部分构成： 一个是跟踪器（tracker）， 一个是存储节点（storage）  