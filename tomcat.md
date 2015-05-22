# 配置 Tomcat 

<span>【**关于**</span>**<span>Tomcat</span>**<span>】</span>

<span>目前有很多网站使用</span><span>jsp</span><span>的程序编写，所以解析</span><span>jsp</span><span>的程序就必须要有相关的软件来完成。</span><span>Tomcat</span><span>就是用来解析</span><span>jsp</span><span>程序的一个软件，</span> <span>Tomcat</span><span>是</span><span>Apache</span> <span>软件基金会（</span><span>Apache Software Foundation</span><span>）的</span><span>Jakarta</span> <span>项目中的一个核心项目，由</span><span>Apache</span><span>、</span><span>Sun</span> <span>和其他一些公司及个人共同开发而成。因为</span><span>Tomcat</span> <span>技术先进、性能稳定，而且免费，因而深受</span><span>Java</span> <span>爱好者的喜爱并得到了部分软件开发商的认可，成为目前比较流行的</span><span>Web</span> <span>应用服务器。</span>

<span>Tomcat</span> <span>是一个轻量级应用服务器，在中小型系统和并发访问用户不是很多的场合下被普遍使用，是开发和调试</span><span>JSP</span> <span>程序的首选。对于一个初学者来说，可以这样认为，当在一台机器上配置好</span><span>Apache</span> <span>服务器，可利用它响应对</span><span>HTML</span> <span>页面的访问请求。实际上</span><span>Tomcat</span> <span>部分是</span><span>Apache</span> <span>服务器的扩展，但它是独立运行的，所以当你运行</span><span>tomcat</span> <span>时，它实际上作为一个与</span><span>Apache</span> <span>独立的进程单独运行的。</span>

<span>【**安装**</span>**<span>Tomcat</span>**<span>】</span>

<span>Tomcat</span><span>的安装分为两个步骤：安装</span><span>JDK</span><span>；安装</span><span>Tomcat</span><span>。</span>

<span>JDK(Java Development Kit)</span><span>是</span><span>Sun Microsystems</span><span>针对</span><span>Java</span><span>开发员的产品。自从</span><span>Java</span><span>推出以来，</span><span>JDK</span><span>已经成为使用最广泛的</span><span>Java SDK</span><span>。</span><span>JDK</span> <span>是整个</span><span>Java</span><span>的核心，包括了</span><span>Java</span><span>运行环境，</span><span>Java</span><span>工具和</span><span>Java</span><span>基础的类库。所以要想运行</span><span>jsp</span><span>的程序必须要有</span><span>JDK</span><span>的支持，理所当然安装</span><span>Tomcat</span><span>的前提是安装好</span><span>JDK</span><span>。</span>

**<span> </span>**

**<span>1\.</span> ****<span>安装</span>****<span>JDK</span>**

<span>下载</span><span>jdk-6u23-linux-i586.bin</span>

<span>cd /usr/local/src/</span>

<span>wget http://dl.dropbox.com/u/182853/jdk-6u23-linux-i586.bin</span>

<span>（如果该版本不合适请到下面的官方网站下载适合你的版本）：</span>

<span>https://cds.sun.com/is-bin/INTERSHOP.enfinity/WFS/CDS-CDS_Developer-Site/en_US/-/USD/ViewProductDetail-Start?ProductRef=jdk-6u23-oth-JPR@CDS-CDS_Developer</span>

<span>chmod a+x jdk-6u23-linux-i586.bin</span>

<span>sh jdk-6u23-linux-i586.bin</span>

<span>此时会出现</span><span>JDK</span> <span>安装授权协议。可以一路按</span><span>Enter</span><span>浏览，当出现</span><span>Do you agree to the above license terms? [yes or no]</span> <span>的字样</span><span>,</span><span>输入</span><span>yes</span><span>即可。</span>

<span>mv  jdk1.6.0_23  /usr/local/</span>

**<span> </span>**

**<span>2\.</span> ****<span>设置环境变量</span>**

<span>vim /etc/profile</span>

<span>在末尾输入以下内容</span><span>
 #set java environment</span>

<span>JAVA_HOME=/usr/local/jdk1.6.0_23/</span>

<span>JAVA_BIN=/usr/local/jdk1.6.0_23/bin</span>

<span>JRE_HOME=/usr/local/jdk1.6.0_23/jre</span>

<span>PATH=$PATH:/usr/local/jdk1.6.0_23/bin:/usr/local/jdk1.6.0_23/jre/bin</span>

<span>CLASSPATH=/usr/local/jdk1.6.0_23/jre/lib:/usr/local/jdk1.6.0_23/lib:/usr/local/jdk1.6.0_23/jre/lib/charsets.jar</span>

<span>export  JAVA_HOME  JAVA_BIN JRE_HOME  PATH  CLASSPATH
</span><span>执行<span>命令</span></span><span>source /etc/profile</span><span>，使配置立即生效</span>

<span>source /etc/profile</span>

<span>检测是否设置正确：</span>

<span>java –version</span>

<span>如果显示如下内容，则配置正确。</span>

<span>java version "1.4.2"</span>

<span>gij (GNU libgcj) version 4.1.2 20080704 (Red Hat 4.1.2-46)</span>

<span> </span>

<span>Copyright (C) 2006 Free Software Foundation, Inc.</span>

<span>This is free software; see the source for copying conditions.  There is NO warranty; not even for MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.</span>

**<span> </span>**

**<span>3.</span>****<span>安装</span>****<span>Tomcat</span>**

<span>cd /usr/local/src/</span>

<span>wget http://archive.apache.org/dist/tomcat/tomcat-7/v7.0.14/bin/apache-tomcat-7.0.14.tar.gz</span>

<span>如果觉得这个版本不适合你，请到</span><span><a>tomcat<span><span>官方网站</span></span></a></span><span>下载适合你的版本。</span>

<span>tar zxvf apache-tomcat-7.0.14.tar.gz</span>

<span>mv apache-tomcat-7.0.14 /usr/local/tomcat</span>

<span>cp -p /usr/local/tomcat/bin/catalina.sh /etc/init.d/tomcat</span>

<span>vim /etc/init.d/tomcat</span>

<span>在第二行加入以下内容：</span>

<span># chkconfig: 2345 63 37</span>

<span># description: tomcat server init script</span>

<span> </span>

<span>JAVA_HOME=/usr/local/jdk1.6.0_23/</span>

<span>CATALINA_HOME=/usr/local/tomcat</span>

<span> </span>

<span>chmod 755 /etc/init.d/tomcat</span>

<span>chkconfig --add tomcat</span>

<span>chkconfig tomcat on</span>

<span> </span>

<span>启动</span><span>tomcat</span><span>：</span>

<span>service tomcat start</span>

<span>查看是否启动成功：</span>

<span>ps aux |grep tomcat</span>

<span>如果有进程的话，请在浏览器中输入</span><span>http://IP:8080/</span> <span>你会看到</span><span>tomcat</span><span>的主界面。</span>

<span>【**配置**</span>**<span>tomcat</span>**<span>】</span>

<span>在配置</span><span>tomcat</span><span>前，先来看看</span><span>tomcat</span><span>的几个目录：</span>

**<span>find /usr/local/tomcat/ -maxdepth 1 -type d</span> ****<span>（</span>**<span>-maxdepth</span><span>的作用指定目录级数，后边跟</span><span>1</span><span>代表只查找</span><span>1</span><span>级目录**）**</span>

<span>/usr/local/tomcat/</span>

<span>/usr/local/tomcat/lib       # tomcat</span><span>的库文件目录</span>

<span>/usr/local/tomcat/temp           #</span> <span>临时文件存放目录</span>

<span>/usr/local/tomcat/webapps             # web</span><span>应用目录，也就是我们访问的</span><span>web</span><span>程序文件所在目录</span>

<span>/usr/local/tomcat/conf             #</span> <span>配置文件目录</span>

<span>/usr/local/tomcat/logs             #</span> <span>日志文件所在目录</span>

<span>/usr/local/tomcat/work            #</span> <span>存放</span><span>JSP</span><span>编译后产生的</span><span>class</span><span>文件</span>

<span>/usr/local/tomcat/bin               # tomcat</span><span>的脚本文件</span>

<span>Tomcat</span><span>的主配置文件为</span><span>/usr/local/tomcat/conf/server.xml</span>

**<span>1\.</span> ****<span>配置</span>****<span>tomcat</span>****<span>服务的访问端口。</span>**

<span>默认是</span><span>8080</span><span>，如果你想修改为</span><span>80</span><span>，则需要修改</span><span>server.xml</span><span>文件。</span>

<span>找到</span> <span><Connector port="8080" protocol="HTTP/1.1"</span>

<span>修改为：</span><span><Connector port="80" protocol="HTTP/1.1"</span>

**<span>2\.</span> ****<span>配置新的虚拟主机</span>**

<span>cd /usr/local/tomcat/conf/</span>

<span>vim server.xml</span>

<span>找到</span><span></Host></span><span>，下一行插入新的</span><span><Host></span><span>，内容如下：</span>

<span>      <Host name="www.example.cn" appBase="/data/tomcatweb"</span>

<span>            unpackWARs="false" autoDeploy="true"</span>

<span>            xmlValidation="false" xmlNamespaceAware="false"></span>

<span>      <Context path="" docBase="./" debug="0" reloadable="true" crossContext="true"/></span>

<span>      </Host></span>

<span>完成后，重启</span><span>tomcat</span>

<span>service tomcat stop; service tomcat start</span>

<span>测试新建的虚拟主机，首先需要修改你电脑的</span><span>hosts</span><span>文件</span>

<span>vim /data/tomcatweb/test.jsp</span> <span>加入以下内容：</span>

<span><html><body><center></span>

<span>Now time is: <%=new java.util.Date()%></span>

<span></center></body></html></span>

<span>保存后，在你的浏览器里输入</span> <span>http://www.example.cn/test.jsp</span> <span>看是否访问到如下内容：</span>

<span>Now time is: Thu Jun 02 14:32:34 CST 2011</span>

<span>上面的</span><span>test.jsp</span><span>就是要显示当前系统的时间。</span>

</div>

