
首先从官网上 http://maven.apache.org/ 下载最新版Maven。我用的是apache-maven-3.0.4-bin.tar.gz。将下载后的文件拷贝到 /usr/local/目录下。

1、执行 tar -zxvf apache-maven-3.0.4-bin.tar.gz 命令解压文件

2、解压后会生成apache-maven-3.0.4目录，删除apache-maven-3.0.4-bin.tar.gz压缩包文件

3、执行 ln -s apache-maven-3.0.4 apache-maven（为Maven做一个软链接，方便以后升级）

4、执行 vi /etc/profile 文件，插入如下内容
```
         export M2_HOME=/usr/local/apache-maven
         export MAVEN_HOME=/usr/local/apache-maven
         PATH=$PATH:$JAVA_HOME/bin:$M2_HOME/bin
```

5、保存并退出VI编辑器，执行 source /etc/profile 命令使改动生效

6、执行 mvn -v 命令，如出现如下内容表示安装配置成功

#使用
下载 “kaptcha”，将其解压缩并将 kaptcha-version.jar 复制到其他地方，比如：C盘。发出下面的命令：
```
mvn install:install-file -Dfile=c:\kaptcha-{version}.jar -DgroupId=com.google.code -DartifactId=kaptcha -Dversion={version} -Dpackaging=jar
```

 安装完毕后，就在 pom.xml 中声明 kaptcha 的坐标。
```
<dependency>
      <groupId>com.google.code</groupId>
      <artifactId>kaptcha</artifactId>
      <version>2.3</version>
 </dependency>
```

 1. mvn help:describe 你是否因为记不清某个插件有哪些goal而痛苦过,你是否因为想不起某个goal有哪些参数而苦恼,那就试试这个命令吧,它会告诉你一切的. 参数: 1. -Dplugin=pluginName 2. -Dgoal(或-Dmojo)=goalName:与-Dplugin一起使用,它会列出某个插件的goal信息,如果嫌不够详细,同样可以加-Ddetail.(注:一个插件goal也被认为是一个 “Mojo”) 下面大家就运行mvn help:describe -Dplugin=help -Dmojo=describe感受一下吧!

2. mvn archetype:generate 你是怎么创建你的maven项目的?是不是像这样:mvn archetype:create -DarchetypeArtifactId=maven-archetype-quickstart -DgroupId=com.ryanote -Dartifact=common,如果你还再用的话,那你就out了,现代人都用mvn archetype:generate了,它将创建项目这件枯燥的事更加人性化,你再也不需要记那么多的archetypeArtifactId,你只需输入archetype:generate,剩下的就是做”选择题”了.

3. mvn tomcat:run 用了maven后,你再也不需要用eclipse里的tomcat来运行web项目(实际工作中经常会发现用它会出现不同步更新的情况),只需在对应目录(如/ryanote)里运行 mvn tomat:run命令,然后就可在浏览器里运行http://localhost:8080/ryanote查看了.如果你想要更多的定制,可以在pom.xml文件里加下面配置: 01 02 03 04 org.codehaus.mojo 05 tomcat-maven-plugin 06 07 /web 08 9090 09 10 11 12 当然你也可以在命令里加参数来实现特定的功能,下面几个比较常用: 1. 跳过测试:-Dmaven.test.skip(=true) 2. 指定端口:-Dmaven.tomcat.port=9090 3. 忽略测试失败:-Dmaven.test.failure.ignore=true 当然,如果你的其它关联项目有过更新的话,一定要在项目根目录下运行mvn clean install来执行更新,再运行mvn tomcat:run使改动生效.

4. mvnDebug tomcat:run 这条命令主要用来远程测试,它会监听远程测试用的8000端口,在eclipse里打开远程测试后,它就会跑起来了,设断点,调试,一切都是这么简单.上面提到的那几个参数在这里同样适用.

5. mvn dependency:sources 故名思义,有了它,你就不用到处找源码了,运行一下,你项目里所依赖的jar包的源码就都有了