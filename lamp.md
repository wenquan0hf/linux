# LAMP 环境搭建

<span>经过前部分章节的学习，你已经掌握了</span><span>linux</span><span>的基础知识了</span><span>。</span><span>但是想成为一名系统管理员恐怕还有点难度，因为好多单位招聘这个职位的时候都要求有一定的工作经验</span><span>。</span><span>然而真正的经验一天两天是学不来的，是靠长时间积累得来的</span><span>。</span><span>不过你也不要灰心，所谓的工作经验无非也就是一些运行在</span><span>linux</span><span>系统上的软件的配置以及应用</span><span>。</span><span>就好像是装在</span><span>windows</span><span>上的</span><span>office</span><span>一样，大部分人都会装，但是十分会用的却不多</span><span>。</span><span>是因为</span><span>office</span><span>太难吗，当然不是，只是因为只有一小部分人花费了很长很长的时间去使用和研究</span><span>office</span><span>而已</span><span>。</span>

<span>LAMP</span> <span>是</span><span>Linux Apache MySQL PHP</span><span>的简写，其实就是把</span><span>Apache, MySQL</span><span>以及</span><span>PHP</span><span>安装在</span><span>Linux</span><span>系统上，组成一个环境来运行</span><span>php</span><span>的脚本语言</span><span>。</span><span>至于什么是</span><span>php</span><span>脚本语言，笔者不再介绍，请自己查资料吧</span><span>。Apache</span><span>是最常用的</span><span>WEB</span><span>服务软件，而</span><span>MySQL</span><span>是比较小型的数据库软件，这两个软件以及</span><span>PHP</span><span>都可以安装到</span><span>windows</span><span>的机器上</span><span>。</span><span>下面笔者就教你如何构建这个</span><span>LAMP</span><span>环境</span><span>。</span>

<span>【</span><span>**安装**</span><span>**MySQL**</span><span>】</span>

<span>一般我们平时安装</span><span>MySQL</span><span>都是</span><span>源码</span><span>包安装的，但是由于它的</span><span>编译</span><span>需要很长的</span><span>时间</span><span>，所以，笔者建议你安装二进制免编译包</span><span>。</span><span>你可以到</span><span>MySQL</span><span>官方网站去</span><span>下载:</span><span><a>http://www.mysql.com/downloads/</a></span><span>具体版本根据你的平台和需求而定，目前比较常用的</span><span>mysql-5.1.x</span> <span>和</span><span>mysql-5.3.x</span><span>下面是安装步骤：</span>

<span>1\.</span> <span>下载</span><span>mysql</span><span>到</span><span>/usr/local/src/</span>

<span>cd /usr/local/src/</span>

<span>wget  http://syslab.comsenz.com/downloads/linux/mysql-5.0.86-linux-i686-icc-glibc23.tar.gz</span>

<span>2\.</span> <span>解压</span>

<span>tar zxvf /usr/local/src/mysql-5.0.86-linux-i686-icc-glibc23.tar.gz</span>

<span>3\.</span> <span>把解压完的</span><span>数据</span><span>移动到</span><span>/usr/local/mysql</span>

<span>mv mysql-5.0.86-linux-i686-icc-glibc23 /usr/local/mysql</span>

<span>4\.</span> <span>建立</span><span>mysql</span><span>用户</span>

<span>useradd mysql</span>

<span>5\.</span> <span>初始化数据库</span>

<span>cd /usr/local/mysql</span>

<span>mkdir /data/mysql ; chown -R mysql:mysql /data/mysql</span>

<span>./scripts/mysql_install_db --user=mysql --datadir=/data/mysql</span>

<span>--user</span><span>定义数据库的所属主，</span><span>--datadir</span><span>定义数据库安装到哪里，建议放到大空间的分区上，这个目录需要自行创建</span><span>。</span>

<span>6\.</span> <span>拷贝配置文件</span>

<span>cp support-files/my-large.cnf /etc/my.cnf</span>

<span>7\.</span> <span>拷贝启动脚本文件并修改其属性</span>

<span>cp support-files/mysql.server  /etc/init.d/mysqld</span>

<span>chmod 755 /etc/init.d/mysqld</span>

<span>8\.</span> <span>修改启动脚本</span>

<span>vim /etc/init.d/mysqld</span>

<span>需要修改的地方有</span><span>datadir=/data/mysql</span><span>（前面初始化数据库时定义的目录）</span>

<span>9\.</span> <span>把启动脚本加入系统服务项，并设定开机启动，启动</span><span>mysql</span>

<span>chkconfig --add mysqld</span>

<span>chkconfig mysqld on</span>

<span>service mysqld start</span>

<span>如果启动不了，请到</span><span>/data/mysql/</span> <span>下查看错误日志，这个日志通常是主机名.err</span><span>。</span><span>关于</span><span>mysql</span><span>的配置文件</span><span>/etc/my.cnf</span><span>请参考这篇文章</span><span><a>http://www.92csz.com/19/603.html</a></span>

<span>【</span><span>**安装**</span><span>**Apache**</span><span>】</span>

<span>cd /usr/local/src/</span>

<span>wget  http://syslab.comsenz.com/downloads/linux/httpd-2.2.11.tar.gz</span>

<span>useradd www</span> <span>（增加</span> <span>Apache</span><span>运行账户）</span>

<span>tar zvxf httpd-2.2.11.tar.bz2</span>

<span>cd httpd-2.2.11</span>

<span>./</span><span>conf</span><span>igure --prefix=/usr/local/apache2 --with-included-apr --enable-so --enable-deflate=shared --enable-expires=shared --enable-rewrite=shared --enable-static-support --disable-userdir</span>

<span>make</span>

<span>make</span> <span>install</span>

<span>【</span><span>**安装**</span><span>**PHP**</span><span>】</span>

<span>wget http://syslab.comsenz.com/downloads/linux/php-5.2.10.tar.gz</span>

<span>tar zvxf</span> <span>php</span><span>-5.2.10.tar.gz
cd php-5.2.10
./</span><span>conf</span><span>igure --prefix=/usr/local/php \ 
--with-apxs2=/usr/local/apache2/bin/apxs \
--with-config-file-path=/usr/local/php/etc \
--with-mysql=/usr/local/mysql \
--with-libxml-dir \
--with-gd \
--with-jpeg-dir \
--with-png-dir \
--with-freetype-dir \
--with-iconv-dir \
--with-zlib-dir  \
--with-bz2 \
--with-openssl \
--with-mcrypt \
--enable-soap \
--enable-gd-native-ttf \
--enable-ftp \
--enable-mbstring \
--enable-sockets \
--enable-exif \
--disable-ipv6 
make && make install
mkdir /usr/local/php/etc
cp php.ini-dist /usr/local/php/etc/php.ini</span>

<span>【</span><span>**apache**</span><span>**结合**</span><span>**php**</span><span>】</span>

<span>Apache</span><span>主配置</span><span>文件</span><span>为：</span><span>/usr/local/apache2/</span><span>conf</span><span>/httpd.conf
# vim /usr/local/apache2/conf/httpd.conf
</span><span>找到：</span><span>
AddType application/x-gzip .gz .tgz
</span><span>在该行下面添加</span><span>
AddType application/x-httpd-</span><span>php</span> <span>.php</span><span>找到：</span><span>
<IfModule dir_module>
    DirectoryIndex index.html
</IfModule>
</span><span>将该行改为</span><span>
<IfModule dir_module>
    DirectoryIndex index.html index.htm index.php
</IfModule>

</span><span>找到：</span><span>
#Include conf/extra/httpd-mpm.conf
#Include conf/extra/httpd-info.conf
#Include conf/extra/httpd-vhosts.conf
#Include conf/extra/httpd-default.conf
</span><span>去掉前面的</span><span>“#”</span><span>号，取消注释</span><span>。</span>

<span>【</span><span>**配置**</span><span>**apache**</span><span>**的进程管理以及虚拟主机**</span><span>】</span>

<span>**1\.** </span><span>**配置**</span><span>**Apache**</span><span>**进程管理**</span><span>
</span><span>配置文件为：</span><span>/usr/local/apache2/conf/extra/httpd-mpm.conf
</span><span>将配置文件中下面一段修改为如下：</span><span><IfModule mpm_prefork_module>
    ServerLimit          2048   </span> <span>新添加</span><span>    StartServers          5
    MinSpareServers      5
    MaxSpareServers      10
    MaxClients           1024</span> <span>默认最大为</span><span>256</span><span>，设置为超过</span><span>256</span><span>必须增加有</span><span>ServerLimit
    MaxRequestsPerChild   0
</IfModule></span>

<span>**2\.** </span><span>**配置**</span><span>**Apache**</span><span>**虚拟主机**</span><span>
</span><span>配置文件为：</span><span>/usr/local/apache2/conf/extra/httpd-vhosts.conf
</span><span>将配置文件中下面一段修改为如下：</span><span><VirtualHost *:80>
   # ServerAdmin</span> <span>webmaster@dummy-host.example.com</span><span>    DocumentRoot "/data/www"
    ServerName</span> <span>www.example.com.cn</span><span>
    ErrorLog "|/usr/local/apache2/bin/rotatelogs -l /www/logs/error.log-%Y%m%d 86400"
   CustomLog "|/usr/local/apache2/bin/rotatelogs -l /www/logs/access.log-%Y%m%d 86400" combined
   </VirtualHost>

</span><span>说明：</span><span>ServerAdmin</span> <span>参数后为管理员</span><span>email
DocumentRoot</span> <span>指的是论坛文件存放的目录</span><span>
ServerName  </span><span>是论坛的域名</span><span>ErrorLog</span> <span>是论坛错误日志</span><span>  </span><span>通过管道使用</span><span>apache</span><span>自带的</span><span>rotatelogs</span><span>工具将日志切割为每天一个文件</span><span>CustomLog</span> <span>是论坛访问日志，同样切割为每天一个文件</span>

<span>配置</span><span>Apache</span><span>缺省</span><span>httpd</span><span>设置</span><span>
</span><span>配置文件为：</span><span>/usr/local/apache2/conf/extra/httpd-default.conf
</span><span>将配置文件中下面一段：</span><span>
</span><span>将</span><span>KeepAlive On</span> <span>改为</span><span>KeepAlive Off
</span>

| 

配置Apache的访问权限
vim /usr/local/apache2/conf/httpd.conf
找到
<Directory />
Options FollowSymlinks
AllowOverride None
Order deny,allow
Deny form all
</Directory>
改成：
<Directory />
Options FollowSymlinks
AllowOverride None
Order deny,allow
Allow form all
</Directory> 
配置Apache的运行账户
vim  /usr/local/apache2/conf/httpd.conf
找到
User  daemon
Group daemon
改成
User www
Group www

 |

<span>配置完上述内容之后，启动</span><span>Apache</span><span>：</span><span>
/usr/local/apache2/bin/apachectl start</span>

<span>【</span><span>**测试**</span><span>**LAMP**</span><span>**是否成功**</span><span>】</span>

<span>vim /data/www/1.php</span>

<span>写入：</span>

<span><?php 
</span><span>phpinfo();
</span><span>?></span>

<span>保存后，然后在浏览器中输入</span> <span>http://</span><span>你配置的域名</span><span>/1.php</span> <span>看是否能看到</span><span>php</span><span>的相关配置信息</span><span>。</span>

<span>【</span><span>**Zend**</span><span>**安装**</span><span>】</span>

<span>有时，需要在你的</span><span>LAMP</span><span>环境中配置</span><span>ZEND</span><span>，因为有些</span><span>php</span><span>的应用程序比如</span><span>Discuz!</span> <span>或者</span><span>phpwind</span><span>等是需要用</span><span>zend</span><span>来解密的，不装</span><span>zend</span><span>会显示乱码</span><span>。</span><span>安装步骤为：</span>

<span>cd /usr/local/src</span>

<span>wget http://syslab.comsenz.com/downloads/linux/ZendOptimizer-3.3.3-linux-glibc23-i386.tar.gz</span>

<span>tar zxvf ZendOptimizer-3.3.3-linux-glibc23-i386.tar.gz</span>

<span>cd ZendOptimizer-3.3.3-linux-glibc23-i386</span>

<span>./install.sh</span>

<span>根据提示安装</span><span>。php.ini文件的路径为：/usr/local/php/etc/ 当提示是否重启apache时，选择不重启。</span>

