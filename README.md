# Ubuntu16.04LTS-JDK-eclipse
因为要学习Java SE，教学要求是eclipse，所以进行了尝试安装，并最终成功运行。


    
系统版本：Ubuntu 16.04 LTS
JDK版本：jdk1.8.0_181

一、安装JDK

1.官网下载 JDK文件：http://download.oracle.com/otn-pub/java/jdk/8u181-b13/96a7b8442fe848ef90c96a2fad6ed6d1/jdk-8u181-linux-x64.tar.gz

2.创建一个目录作为JDK的安装目录，我的目录为 /opt/java
sudo mkdir /opt/java

3.移动文件到/opt/java目录下
sudo mv jdk-8u121-linux-x64.tar.gz /opt/java

4.解压文件
tar -zxvf jdk-8u121-linux-x64.tar.gz

5.配置环境变量
sudo gedit /etc/environment

末尾加入以下配置（JAVA_HOME 后的路径就是jdk的文件位置）

PATH="/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:$JAVA_HOME/bin"
export CLASSPATH=.:$JAVA_HOME/lib:$JAVA_HOME/jre/lib
export JAVA_HOME=/opt/java/jdk1.8.0_121

修改完成之后保存关闭，并输入以下命令使环境变量立即生效
source /etc/environment

6.还需要配置所有用户的环境变量
sudo gedit /etc/profile

在文件的最后添加以下内容：
#set Java environment
export JAVA_HOME=/opt/java/jdk1.8.0_121
export JRE_HOME=$JAVA_HOME/jre
export CLASSPATH=.:$JAVA_HOME/lib:$JRE_HOME/lib:$CLASSPATH
export PATH=$JAVA_HOME/bin:$JRE_HOME/bin:$PATH

7.同样，需要使用命令使环境变量立即生效
source /etc/profile

8.输入java -version，显示JDK版本说明恭喜你，环境变量配置正确
截图

9.重启电脑，能正常进入系统，且 java -version 命令有效
Eclipse 安装及配置

二、安装eclipse

1.官网下载 Eclipse IDE for Java EE Developers（64位）：http://www.eclipse.org/downloads/download.php?file=/technology/epp/downloads/release/2018-09/R/eclipse-jee-2018-09-linux-gtk-x86_64.tar.gz
![image](https://github.com/ArthurCaoMH/Ubuntu16.04LTS-JDK-eclipse/blob/master/pictures/eclipse_java_ee.png)
这里最好还是要用什么就下什么包，大家都知道 Eclipse Installer 这个安装包在没有外网的情况下是基本废的

2.安装 eclipse 将其解压到/opt/文件夹中
sudo tar zxvf eclipse-jee-neon-2-linux-gtk-x86_64.tar.gz -C /opt

3.创建eclipse桌面快捷方式图标。
cd ~/桌面
sudo touch eclipse.desktop
sudo vim eclipse.desktop

输入以下内容：
[Desktop Entry]
Encoding=UTF-8
Name=Eclipse
Comment=Eclipse
Exec=/opt/eclipse/eclipse
Icon=/opt/eclipse/icon.xpm
Terminal=false
StartupNotify=true
Type=Application
Categories=Application;Development;

保存。
执行：sudo chmod 775 eclipse.desktop 将其变为可执行文件.

4.在桌面打开 eclipse ，结果提示没有安装JDK，JRE环境，明明我们安装过。

解决方法：见下文
Eclipse 启动报错 (或)
使用 Java Installer 执行eclipse-inst 报错

此情况下会出现如下内容：

    A Java RunTime Environment (JRE) or Java Development Kit (JDK) must be available in order to run Eclipse. No java virtual machine was found after searching the following locations:…

解决办法：

1.在终端进入你的eclipse目录（如果是启动 Java Installer 则进入相应的目录）
2.然后输入：
mkdir jre
cd jre
ln -s /opt/java/jkd1.8.0_121/bin/（这里是你安装 Java 的路径）

后记

这里我把软件都装在了 /opt 路径下，个人习惯。通常情况，请不要直接装在这个路径下。因为 /opt 一般只有root用户才能访问，如果开发时使用的时普通用户，会很麻烦。
