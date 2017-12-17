# Setup

## Java

配置java：主要JAVA_HOME中不能有末尾分号，否则报错javac不是内部命令，利用java，javac可以检测是否安装成功。

jdk-8u131-windows-x64.exe安装时直接点击下载一路确定即可。

变量名：JAVA_HOME
变量值：C:\Program Files (x86)\Java\jdk1.8.0_91        // 注意千万不能后面有分号，要根据自己的实际路径配置
变量名：CLASSPATH
变量值：.;%JAVA_HOME%\lib\dt.jar;%JAVA_HOME%\lib\tools.jar;         //记得前面有个"."
变量名：Path
变量值：%JAVA_HOME%\bin;%JAVA_HOME%\jre\bin;


## Scala
配置scala：还是注意home中不能有末尾分号，利用scala可以检测是否安装成功。

scala-2.12.2.msi安装时直接点击下载一路确定即可。

变量名：SCALA_HOME
变量值：C:\Program Files (x86)\scala        // 要根据自己的实际路径配置
变量名：PATH
变量值：%SCALA_HOME%\bin;%SCALA_HOME%\jre\bin;
变量名：ClassPath
变量值：.;%SCALA_HOME%\bin;%SCALA_HOME%\lib\dt.jar;%SCALA_HOME%\lib\tools.jar;

## Maven
利用mvn -version可以检测是否安装成功。
Maven是一个强大的Java项目构建工具：一个用来把源代码构建成可发布的构件的工具。
对于java与scala，需要将源文件（.java、.scala）编译为class字节码文件(.class)，以便在解释器上执行。

apache-maven-3.5.0-bin.zip直接解压缩到指定的文件夹即可。

变量名：MAVEN_HOME
变量值：C:\Program Files\Maven\apache-maven-3.5.0        // 要根据自己的实际路径配置
变量名：Path
变量值：%MAVEN_HOME%\bin;

###构建工具作用
构建工具是将软件项目构建相关的过程自动化的工具。构建一个软件项目通常包含以下一个或多个过程：
生成源码（如果项目使用自动生成源码）；
从源码生成项目文档；
编译源码；
将编译后的代码打包成JAR文件或者ZIP文件；
将打包好的代码安装到服务器、仓库或者其它的地方；
有些项目可能需要更多的过程才能完成构建，这些过程一般也可以整合到构建工具中，因此它们也可以实现自动化。

##References
- [Java开发环境配置](http://www.runoob.com/java/java-environment-setup.html)
- ['JAVAC'不是内部或外部命令解决方法](http://jingyan.baidu.com/article/1e5468f924210a484961b7f0.html)