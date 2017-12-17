# Intellij
## 1.Setup
### 安装细节
1）安装时：社区版（Community Edition）为免费版本。其中有选项表示关联 Java 和 Groovy 文件，建议都不要勾选，正常我们会在 Windows 的文件系统上打开这类文件都是为了快速查阅文件里面的内容，如果用 IntelliJ IDEA 关联上之后，由于 IntelliJ IDEA 打开速度缓慢，这并不能方便我们查看。

2）首次启动：第三个单选按钮表示你没有任何早期版本的 IntelliJ IDEA 配置，你不导入任何配置，让 IntelliJ IDEA 生成一份新的配置。

### 配置
1）对于这个设置目录（C:\Users\Jimmy\.IdeaIC2017.2）有一个特性，就是你删除掉整个目录之后，重新启动 IntelliJ IDEA 会再自动帮你再生成一个全新的默认配置，所以很多时候如果你把 IntelliJ IDEA 配置改坏了，没关系，删掉该目录，一切都会还原到默认，建议新人可以多自己摸索 IntelliJ IDEA 的配置，多几次还原，有助于加深对 IntelliJ IDEA 的了解。

2）安装scala插件：Configure-Plugins-Install JetBrains plugin；搜索"scala"；点击Install进行安装。
J如果没有就下载下来然后本地安装，有选项install from local disk。

3）全局配置java的sdk：Configure-Project Defaults-Project Structure；Default Project Structure中Project-New-JDK；选中JAVA_HOME的目录。
**J设置完后，如果没有项目，重新打开还是没有选中状态，先创建项目之后就会固定了。**

4）全局配置scala自身sdk：Configure-Project Defaults-Project Structure；Default Project Structure中Global Libraries-加号-Scala SDK；选中系统本身所安装的Scala（即System对应的版本）；中间一栏位置处出现Scala的SDK，在其上右键点击后选择Copy to Project Libraries，这个操作是为了将Scala SDK添加到项目的默认Library中去。
**J这个操作一开始没有项目时候是始终没有反应的，需要先新建一个项目，然后进入项目后点击菜单中的project structure。然后再重复上述操作。此时点击Copy to Project Libraries，会有problemn提示该scala is not used。不用管它。等将Scala的框架添加到这个项目后，就会消失problem。**

## 2.基础知识
###Maven有一个标准的目录结构：如果你在项目中遵循Maven的目录结构，就无需在pom文件中指定源代码、测试代码等目录。
1.src目录是源代码和测试代码的根目录。
2.src目录下的main目录是应用的源代码目录。src目录下的test目录是测试代码的目录。main和test下的java目录，分别表示应用的java源代码和测试代码。
3.resources目录包含项目的资源文件，比如应用的国际化配置的属性文件等。
4.target目录是由Maven创建的，其中包含编译后的类文件、jar文件等。当执行maven的clean目标后，target目录会被清空。

###intellij左侧的目录面板会把当前项目文件夹下的所有子文件夹都显示出来。
1.比如.idea文件夹，创建项目的时候自动创建一个 .idea 的项目配置目录来保存项目的配置信息。这是默认选项。
2.比如文件.iml 即为 Module 的配置文件。

###Source root的作用是标记该目录下的文件是可编译的。J理解为maven会对其进行编译。
此外设置Source root主要意思是将 scala 文件夹标记为一个源文件的根目录，然后在其内的所有代码中的 package ，其路径就从这个根目录下开始算起。举个例子，假如你在 scala 文件夹中建立了一个程序，这个程序的 package属性为com.abc.test，那么这个程序就一定要保存在 scala\com\abc\test目录下或者直接是scala\com.abc.test文件名也可以，否则项目就找不到这个程序了。

补充知识：
而package的作用是模块化以使得耦合性降低。
软件开发过程减小程序之间的“耦合性”至关重要，降低耦合性的一个方法是模块化。
Scala的包和Java中的包或者C++中的命名空间的目的是相同的：管理大型程序中的名称。举例来说，Map这个名称可以同时出现在scala.collection.immutable和scala. collection.mutable包而不会冲突。要访问它们中的任何一个，你可以使用完全限定的名称scala.collection.immutable.Map或scala.collection.mutable.Map，也可以使用引入语句来提供一个更短小的别名。

###新建项目
**GroupId，可以理解为用来标志你整个项目组的，或者你这些代码属于某一个完整的项目。一般来说可以使用倒序的公司网址来作为GroupId。比如：com.music.search。**
ArtifactId，一般是用来在整个项目组来标志本项目的。**J这个会作为项目文件夹名放在目录IdeaProjects下。**比如sequent_behavior。
Version，正如字面意思，就是本项目的迭代版本的信息，**不用填写。**

补充知识：
在新建项目时，也可以选择骨架创建。
手动创建Maven项目时，我们是一步步手动来创建Maven项目的骨架的，如src\main\java、src\test\java、pom.xml等等，Maven中我们可以直接使用`mvn archetype:generate`命令来生成一个Maven的骨架。
**J理解为骨架就是符合maven构建要求的文件夹目录。**
没有找到特别推荐的spark的骨架，选择`org.scala-tools.archetypes:scala-archetype-simple`会报错。放弃。还是选择不使用骨架，按照默认方式创建。

默认生成pom.xml：
```xml
	<?xml version="1.0" encoding="UTF-8"?>
	<project xmlns="http://maven.apache.org/POM/4.0.0"
	         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
	    <modelVersion>4.0.0</modelVersion>

	    <groupId>com.music.search</groupId>
	    <artifactId>sequent_behavior</artifactId>
	    <version>1.0-SNAPSHOT</version>
	</project>
```

##3.常用流程
**<u>1）创建Maven工程：Create New Project->Maven；</u>**

**<u>2）填写字段，随便填。</u>**

**<u>3）删除无关文件夹：删除main\java, main\resources 和 test文件夹</u>**

**<u>4）对项目添加scala框架：项目名上右键—Add Framework Support-勾选Scala，确定，这个时候在external libraries中就会显示出scala。</u>**

**<u>5）在main文件夹中建立一个名为scala的文件夹，右键Make Directory as-Sources Root</u>** 

**<u>6）新建scala文件：右键New-然后选择Scala Class；输入名字，Object；</u>**

**<u>7）运行程序：任意位置右键单击-Run '程序名称'。</u>**


## References
- [Scala中包含义](http://www.cnblogs.com/sunddenly/p/4436897.html)
- [降低耦合性的一个方法是模块化](http://wiki.jikexueyuan.com/project/scala-development-guide/use-package.html)