## install pip
sudo python -m ensurepip

##install awscli and modify path variable to let awscli executable
export PATH=~/Library/Python/3.6/bin:$PATH

sudo ssh -i ~/Downloads/awskeypair/wckey.pem ec2-user@ec2-13-58-209-93.us-east-2.compute.amazonaws.com

# wget --no-cookies --no-check-certificate --header "Cookie: gpw_e24=http%3A%2F%2Fwww.oracle.com%2F; oraclelicense=accept-securebackup-cookie" http://download.oracle.com/otn-pub/java/jdk/8u151-b12/e758a0de34e24606bca991d704f6dcbf/jdk-8u151-linux-x64.rpm

# rpm -ivh jdk-8u151-linux-x64.rpm

3.配置JAVA_HOME,CLASSPATH,PATH环境变量

#vi /etc/profile

export JAVA_HOME=/usr/java/jdk1.8.0_151

export PATH=$PATH:$JAVA_HOME/bin

export CLASSPATH=.:$JAVA_HOME/lib

#source /etc/profile

4. setup Tomcat
#wget http://mirror.its.dal.ca/apache/tomcat/tomcat-8/v8.5.23/bin/apache-tomcat-8.5.23.zip

~/apache-tomcat-8.5.23/bin/startup.sh


http://ec2-13-58-209-93.us-east-2.compute.amazonaws.com:8080/TestDemo


## Steps of changing the Tomcat Port
1) Locate server.xml in {Tomcat installation folder}\ conf \

2) Find following similar statement

<!-- Define a non-SSL HTTP/1.1 Connector on port 8180 -->
   <Connector port="8080" maxHttpHeaderSize="8192"
              maxThreads="150" minSpareThreads="25" maxSpareThreads="75"
              enableLookups="false" redirectPort="8443" acceptCount="100"
              connectionTimeout="20000" disableUploadTimeout="true" />
or

<!-- A "Connector" represents an endpoint by which requests are received
     and responses are returned. Documentation at :
     Java HTTP Connector: /docs/config/http.html (blocking & non-blocking)
     Java AJP  Connector: /docs/config/ajp.html
     APR (HTTP/AJP) Connector: /docs/apr.html
     Define a non-SSL HTTP/1.1 Connector on port 8080
-->
<Connector port="8080" protocol="HTTP/1.1"
           connectionTimeout="20000"
           redirectPort="8443" />
3) About Tomcat’s server.xml file cites it’s runs on port 8080. Change the Connector port=”8080″ port to any other port number.

For example

<Connector port="8181" protocol="HTTP/1.1"
              connectionTimeout="20000"
              redirectPort="8443" />
Above statement instruct Tomcat server runs on port 8181.

4) Edit and save the server.xml file. Restart Tomcat. Done



如何在Amazon EC2 Linux(Redhat)实例上搭建JDK,Tomcat环境

一。系统环境：

Linux version 3.10.42-52.145.amzn1.x86_64

卸载OpenJDK

#java -version

java version "1.6.0_24"

OpenJDK Runtime Environment (IcedTea6 1.11.1) (rhel-1.45.1.11.1.el6-x86_64)

OpenJDK 64-Bit Server VM (build 20.0-b12, mixed mode)

#rpm -qa |grep java

java-1.6.0-openjdk-1.6.0.0-1.45.1.11.1.el6.x86_64

tzdata-java-2012c-1.el6.noarch

#rpm -e --nodeps java-1.6.0-openjdk-1.6.0.0-1.45.1.11.1.el6.x86_64

#rpm -qa |grep java

tzdata-java-2012c-1.el6.noarch

#rpm -e --nodeps tzdata-java-2012c-1.el6.noarch

#rpm -qa |grep java

#java -version

bash: /usr/bin/java: 没有那个文件或目录

二。软件、文件准备：

tomcat服务器:apache-tomcat-6.0.41.zip

日志库：log4j-1.2.17.jar

Amazon API认证文件：credentials

JDK安装包：jdk-7u67-linux-x64.rpm

工程文件：

TestDemo.war

三、环境安装：安装JDK,安装Tomcat并配置

1.下载JDK8

wget --no-cookies --no-check-certificate --header "Cookie: gpw_e24=http%3A%2F%2Fwww.oracle.com%2F; oraclelicense=accept-securebackup-cookie" http://download.oracle.com/otn-pub/java/jdk/8u151-b12/e758a0de34e24606bca991d704f6dcbf/jdk-8u151-linux-x64.rpm

2.安装JDK7

#rpm -ivh jdk-8u151-linux-x64.rpm

说明：JDK默认会安装到/usr/java/目录下

3.配置JAVA_HOME,CLASSPATH,PATH环境变量

#vi /etc/profile

export JAVA_HOME=/usr/java/jdk1.8.0_151

export PATH=$PATH:$JAVA_HOME/bin

export CLASSPATH=.:$JAVA_HOME/lib

#source /etc/profile

4.下载Tomcat8,

#wget http://mirror.its.dal.ca/apache/tomcat/tomcat-8/v8.5.23/bin/apache-tomcat-8.5.23.zip

5.解压Tomcat8，并在[tomcat]/bin/cataline.sh文件开始加入：JAVA_OPTS='-Xms512m -Xmx512m'

#将[tomcat]/webapps目录下与项目不相关的文件和文件夹删除，为了安全

#将log4j-1.2.17.jar文件拷贝到[tomcat]/lib目录下

#注意：这里解压完Tomcat通常要启动一下Tomcat，测试一下能否通过外网访问，如果不能需要给Instance添加安全策略

6.设置Tomcat开机启动

修改[tomcat]/bin目录下文件权限为可执行

#chmod 755 *

在/etc/rc.d/rc.local中加入:

#vi /usr/local/tomcat/bin/

如：/usr/local/tomcat/bin/startup.sh

7.启动Tomcat并测试

服务启动过后访问：http://ec2-ip.us-west-2.compute.amazonaws.com:8080/

在TOMCAT中部署war
1、将war文件拷贝到tomcat目录\webapps\ 下。

2、将必要的jar文件拷贝到tomcat目录\lib\ 下。

3、修改tomcat目录\conf\下的server.xml。

<!-- Tomcat Manager Context -->
<Context path="/manager" docBase="manager"debug="0"privileged="true"/>

将这段代码中的
<Context path="/manager" docBase="manager" debug="0"privileged="true"/>
拷贝一下并修改：path="" 为war路径，docBase=""为你的war的文件名。

4、完毕，启动tomcat

